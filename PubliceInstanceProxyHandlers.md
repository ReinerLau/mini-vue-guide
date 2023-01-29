`src/runtime-core/componentPublicInstance.ts`

提取组件代理对象的逻辑
```ts
export const PubliceInstanceProxyHandlers = {
	get(target, key){
		const { setupState } = instance
		if(key in setupState){
			return setupState[key]	
		}
		if(key === '$el'){
			return instance.vnode.el
		}
	}
}
```

获取 instance
```diff
export const publicInstanceProxyHandler = {
+	get({_: instance}, key){
		 const { setupState } = instance
		 if(key in setupState){
			   return setupState[key]
		 }
		if(key === '$el'){
			return instance.vnode.el
		}
	}
}
```