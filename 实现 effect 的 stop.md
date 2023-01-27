```ts
export function stop(runner) {
  runner._effect.stop();
}
```

[[实现 effect 的 scheduler]]
```diff
export function effect(fn, options: any = {}) {
  const _effect = new ReactiveEffect(fn, options.scheduler);
  _effect.run();
+ const runner: any = _effect.run.bind(_effect);
+ runner._effect = _effect;

+ return runner;
}
```

[[实现 effect 的 scheduler]]
```diff
class ReactiveEffect {
  private _fn: any;
+ deps = [];
  scheduler?: Function;

  constructor(fn, scheduler?) {
    this._fn = fn;
    this.scheduler = scheduler;
  }

  run() {
    activeEffect = this;
    return this._fn();
  }

+ stop() {
+   effect.deps.forEach((dep: any) => {
+    dep.delete(effect);
+   });  
+ }
}
```

[[实现收集依赖]]
```diff
export function track(target, key) {
  let depsMap = targetMap.get(target);
  if (!depsMap) {
    depsMap = new Map();
    targetMap.set(target, depsMap);
  }
  let dep = depsMap.get(key);
  if (!dep) {
    dep = new Set();
    depsMap.set(key, dep);
  }

+ if (!activeEffect) return;

  dep.add(activeEffect);
+  activeEffect.deps.push(dep);
}
```