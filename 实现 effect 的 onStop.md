[[实现 effect 的 stop]]
```diff
export function effect(fn, options: any = {}) {
  const _effect = new ReactiveEffect(fn, options.scheduler);
+ Object.assign(_effect, options);

  _effect.run();

  const runner: any = _effect.run.bind(_effect);
  runner._effect = _effect;

  return runner;
}
```

[[重构 effect 的 stop]]
```diff
class ReactiveEffect {
  private _fn: any;
  deps = [];
  active = true;
+ onStop?: () => void;
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
    if (this.active) {
      cleanupEffect(this);
+     if (this.onStop) {
+       this.onStop();
+     }
      this.active = false;
    }
  }
}
```