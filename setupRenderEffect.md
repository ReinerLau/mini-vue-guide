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

[[patch]]

