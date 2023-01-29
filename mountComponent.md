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

传组件的 vnode 给 setupRenderEffect 来保存根节点上的元素
```diff
function mountComponent(vnode, container){
	const instance = createComponentInstance(vnode)
	setupComponent(instance)
+	setupRenderEffect(instance, vnode, container)
}
```

[[createComponentInstance]]
[[setupComponent]]
[[setupRenderEffect]]