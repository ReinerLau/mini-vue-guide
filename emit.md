`src/runtime-core/componentEmit.ts`

# 实现组件 emit
```ts
export function emit(event){
	console.log(event)
}
```

触发事件
```diff
+ export function emit(instance, event){
+	const { props } = instance
+	const handler = props['onAdd']
+	handler && handler()
}
```

改成通用
```diff
export function emit(instance, event){
	const { props } = instance
+	const captilize = (str) => str.charAt(0).toUpperCase() + str.slice(1)
+   const toHandlerKey = (str) => str ? 'on' + captilize(str) : ''
+	const handler = props[toHandlerKey(event)]
	handler && handler()
}
```

传递参数
```diff
+ export function emit(instance, event, ...args){
	const { props } = instance
	const captilize = (str) => str.charAt(0).toUpperCase() + str.slice(1)
	const toHandlerKey = (str) => str ? 'on' + captilize(str) : ''
	const handler = props[toHandlerKey(event)]
+	handler && handler(...args)
}
```

烤肉串改成驼峰
```diff
export function emit(instance, event, ...args){
	const { props } = instance
+	const camelize = (str) => {
+		 return str.replace(/-(\w)/, (_, c) => {
+		   return c ? c.toUpperCase() : ''
+		 })
+	}
	const captilize = (str) => str.charAt(0).toUpperCase() + str.slice(1)
	const toHandlerKey = (str) => str ? 'on' + captilize(str) : ''
+	const handler = props[toHandlerKey(camelize(event))]
	hanlder && handler(...args)
}
```

提取工具函数
```diff
+ import { toHanlderKey, camelize } from '../shared/index'
export function emit(instance, event, ...args){
	const { props } = instance
	const handler = props[toHandlerKey(camelize(event))]
	handler && handler(...args)
}
```

[[toHandlerKey#实现组件 emit]]
[[camelize#实现组件 emit]]