`src/runtime-core/renderer.ts`
```ts
function mountChildern(vnode, el) {
  vnode.children.forEach((v) => {
    patch(v, el);
  });
}
```
[[patch]]