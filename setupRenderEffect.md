# 初始化 component

```ts
function setupRenderEffect(instance, container) {
  const subTree = instance.render();

  patch(subTree, container);
}
```

[[patch#初始化 component]]