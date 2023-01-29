`src/runtime-core/component.ts`

创建组件实例
```ts
export function createComponentInstance(vnode) {
  const component = {
    vnode,
    type: vnode.type,
  };

  return component;
}
```