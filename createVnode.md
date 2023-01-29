元素或组件对象转换为 vnode
```ts
export function createVnode(type, props?, children?) {
  const vnode = {
    type,
    props,
    children,
  };
  return vnode;
}
```

保存根节点元素
```diff
export function createVnode(type, props?, children?){
	const vnode = {
		 type,
		 props,
		 children,
+		 el: null
	}
	return vnode
}
```