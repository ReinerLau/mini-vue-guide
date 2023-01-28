# 初始化 element

```ts
function mountChildern(vnode, el) {
  vnode.children.forEach((v) => {
    patch(v, el);
  });
}
```

[[patch#初始化 element]]