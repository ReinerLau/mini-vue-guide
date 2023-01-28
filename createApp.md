# 初始化 component
`src/runtime-core/createApp.ts`
```ts
import { render } from "./renderer";
import { createVnode } from "./vnode";
export function createApp(rootComponent) {
  return {
    mount(rootContainer) {
      const vnode = createVnode(rootComponent);

      render(vnode, rootContainer);
    },
  };
}
```
[[createVnode#初始化 component]]
[[render#初始化 component]]