`src/shared/index.ts`

# 实现组件 emit

```ts
export function camelize(str){
	return str.replace(/-(\w)/, (_, c) => {
		return c ? c.toUpperCase() : ''
	})	
}
```