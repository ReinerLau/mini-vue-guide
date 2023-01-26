[[实现 effect]]
```diff
export function effect(fn) {
  const _effect = new ReactiveEffect(fn);
  _effect.run();

+ return _effect.run.bind(_effect);
}
```

[[实现 effect]]
```diff
class ReactiveEffect {
  private _fn: any;

  constructor(fn) {
    this._fn = fn;
  }

  run() {
    activeEffect = this;
+   return this._fn();
  }
}
```