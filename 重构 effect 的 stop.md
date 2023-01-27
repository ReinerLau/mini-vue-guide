[[实现 effect 的 stop]]
```diff
class ReactiveEffect {
  private _fn: any;
  deps = [];
+ active = true;
  scheduler?: Function;

  constructor(fn, scheduler?) {
    this._fn = fn;
    this.scheduler = scheduler;
  }

  run() {
    activeEffect = this;
    return this._fn();
  }

  stop() {
+   if (this.active) {
+     cleanupEffect(this);
+     this.active = false;
+   }
  }
}

+ function cleanupEffect(effect) {
+   effect.deps.forEach((dep: any) => {
+     dep.delete(effect);
+   });
+ }
```