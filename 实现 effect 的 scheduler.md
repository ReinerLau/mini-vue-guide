[[实现 effect 返回 runner]]
```diff
+ export function effect(fn, options: any = {}) {
+ const _effect = new ReactiveEffect(fn, options.scheduler);
  _effect.run();

  return _effect.run.bind(_effect);
}
```

[[实现 effect 返回 runner]]
```diff
class ReactiveEffect {
  private _fn: any;
+ public scheduler: Function | undefined;

+ constructor(fn, scheduler?) {
    this._fn = fn;
+   this.scheduler = scheduler;
  }

  run() {
    activeEffect = this;
    return this._fn();
  }
}
```

[[实现触发依赖]]
```diff
export function trigger(target, key) {
  let depsMap = targetMap.get(target);
  let dep = depsMap.get(key);

  for (const effect of dep) {
+   if (effect.scheduler) {
+     effect.scheduler();
+   } else {
      effect.run();
+   }
  }
}
```