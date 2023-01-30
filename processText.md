`src/runtime-core/renderer.ts`

# 实现 Text 类型节点

```ts
function processText(vnode, container){
	const { children } = vnode
	const el = (vnode.el = document.createTextNode(children))
	container.append(el)
}
```