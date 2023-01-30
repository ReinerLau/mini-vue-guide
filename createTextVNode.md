`src/runtime-core/vnode.ts`

# 实现 Text 类型节点

```ts
export function createTextVNode(text){
	return createVnode(Text, {}, text)
}
```

[[createVnode]]
[[Text]]