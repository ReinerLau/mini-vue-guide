`src/runtime-core/renderer.ts`

获取组件实例生成的虚拟节点，然后继续递归拆箱
```ts
function setupRenderEffect(instance, container) {
  const subTree = instance.render();

  patch(subTree, container);
}
```

将 render 的 this 指向组件实例上的代理对象，实现通过 this 返回 setup 返回的结果
```diff
function setupRenderEffect(instance, container){
+	const { proxy } = instance
+	const subTree = instance.render.call(proxy)
	patch(subTree, container)
}
```

patch 之后已经保存组件根节点上的元素，赋值给组件 vnode 的 el
```diff
+ function setupRenderEffect(instance, vnode, container){
	const { proxy } = instance
	const subTree = instance.render.call(proxy)
	patch(subTree, container)
+	vnode.el = subTree.el
}
```

优化可读性
```diff
+ function setupRenderEffect(instance, initialVNode, container){
	const { proxy } = instance	
	const subTree = instance.render.call(proxy)
	patch(subTree, container)
+	initialVNode.el = subTree.el
}
```


[[patch]]

