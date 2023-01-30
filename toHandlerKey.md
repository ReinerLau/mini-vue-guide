`src/shared/index.ts`

# 实现组件 emit

```ts
export function toHandlerKey(str){
	return str ? 'on' + captilize(str) : ''
}
```

[[captilize#实现组件 emit]]