处理自增 ++ 和自减 -- 的情况，这种情况先触发了 get 收集依赖再触发 set 触发依赖，前面触发的 stop 相当于失效了

[[实现 effect 的 stop]]
```diff
let activeEffect;
+ let shouldTrack;

export function track(target, key) {
+ if (!isTracking()) return;
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

  dep.add(activeEffect);
  activeEffect.deps.push(dep);
}

+ function isTracking() {
+  return shouldTrack && activeEffect;
+ }
```

[[重构 effect 的 stop]]
```diff
let activeEffect;
+ let shouldTrack;

class ReactiveEffect {
  private _fn: any;
  deps = [];
  active = true;
  onStop?: () => void;
  scheduler?: Function;

  constructor(fn, scheduler?) {
    this._fn = fn;
    this.scheduler = scheduler;
  }

  run() {
+   if (!this.active) {
+     return this._fn();
+   }
+   shouldTrack = true;
    activeEffect = this;
+   const result = this._fn();
+   shouldTrack = false;
+   return result
  }

  stop() {
    if (this.active) {
      cleanupEffect(this);
      this.active = false;
    }
  }
}
```