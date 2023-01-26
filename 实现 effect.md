```ts
class ReactiveEffect {
  private _fn: any;
  constructor(fn) {
    this._fn = fn;
  }
  run() {
    this._fn();
  }
}
```

```ts
export function effect(fn) {
  const _effect = new ReactiveEffect(fn);
  _effect.run();
}
```