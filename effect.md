### 完整代码

使用 [[ReactiveEffect]] 类创建 effect 实例并立即调用一次回调
```ts
export function effect(fn) {
  const _effect = new ReactiveEffect(fn);
  _effect.run();
}
```