# 初始化 component

```ts
function mountComponent(vnode, container) {
  const instance = createComponentInstance(vnode);

  setupComponent(instance);
  setupRenderEffect(instance, container);
}
```

[[createComponentInstance#初始化 component]]
[[setupComponent#初始化 component]]
[[setupRenderEffect#初始化 component]]