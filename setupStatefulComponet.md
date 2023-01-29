`src/runtime-core/component.ts`

获取setup返回结果
```ts
function setupStatefulComponent(instance) {
  const Component = instance.type;

  const { setup } = Component;

  if (setup) {
    const setupResult = setup();

    handleSetupResult(instance, setupResult);
  }
}
```
[[handleSetupResult]]

创建代理对象绑定到组件实例上，再将组件实例上的 render 的 this 指定为该代理对象
```diff
function setupStatefulComponet(){
	const Component = instance.type
+	instance.proxy = new Proxy({}, {
+		 get(target, key){
+			const { setupState } = instance
+			if(key in setupState){
+			   return setupState[key]
+			}
+		 }
+	})
	const { setup } = Component
	if(setup){
		const setupResult = setup()
		handleSetupResult(instance, setupResult)
	}

}
```

