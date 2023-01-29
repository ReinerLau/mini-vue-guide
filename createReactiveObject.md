`src/reactivity/reactive.ts`

# 实现 readonly

```ts
function createReactiveObject(raw, baseHandlers){
	return new Proxy(raw, baseHandlers)
}
```

# 实现组件接收 props

防止接收的 props 不是对象
```diff
import { isObject } from '../shared/index'
function createReativeObject(raw, baseHandlers){
+	if(isObject(raw)){
+		console.warn(`${raw} is not object`)
+	}
	return new Proxy(raw, baseHandlers)
}
```