# 完整代码

```ts
class ReactiveEffect {
  private _fn: any;

  constructor(fn) {
    this._fn = fn;
  }

  run() {
    activeEffect = this;
    this._fn();
  }
}
```

# run

1. [[实现 reactive#get|get]]

