`src/runtime-core/componentPublicInstance.ts`

# 实现组件代理对象

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

为了方便拓展其他 api
```diff
+ const publicPropertiesMap = {
+	$el: (i) => i.vnode.el
+ }
export const PublicInstanceProxyHandler = {
	get({ _: instance}, key){
		 const { setupState } = instance 
		 if(key in setupState){
			   return setupState[key]
		 }
+		const publicGetter = publicPropertiesMap[key]
+		if(publicGetter){
+			 return publicGetter(instance)
+		}
	}
}
```