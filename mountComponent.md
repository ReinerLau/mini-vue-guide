`src/runtime-core/renderer.ts`

挂载组件
```ts
import { createComponentInstance, setupComponent } from './component.ts'
function mountComponent(vnode, container) {
  const instance = createComponentInstance(vnode);

  setupComponent(instance);
  setupRenderEffect(instance, container);
}
```
[[createComponentInstance]]
[[setupComponent]]
[[setupRenderEffect]]