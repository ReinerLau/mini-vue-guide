# 完整代码

```ts
export function effect(fn) {
  const _effect = new ReactiveEffect(fn);
  _effect.run();
}
```

# run

[[ReactiveEffect#run|ReactiveEffect]]
