`src/runtime-core/createApp.ts`

挂载根组件
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
[[createVnode]]
[[render]]