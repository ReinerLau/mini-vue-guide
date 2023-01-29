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

# 实现组件接收 props

```diff
export function createComponentInstance(vnode){
	const component = {
		vnode,
		type: vnode.type,
+		props: {} 
	}
	return component
}
```