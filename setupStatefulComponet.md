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

# 实现组件代理对象

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

通过 this.$el 访问组件根节点上的元素
```diff
function setupStatefullComponent(instance){
	const Component = instance.type
	instance.proxy = new Proxy({}, {
		 get(target, key){
			const { setupState } = instance
			if(key in setupState){
				return setupState[key]
			}
+			if(key === '$el'){
+				return instance.vnode.el
+			}
		 }
	})
	const { setup } = Component
	if(setup){
		 const setupResult = setup()
		 handleSetupResult(instance, setupResult)
	} 
}
```

提取代理对象的获取器逻辑
```diff
+ import { PublicInstanceProxyHandlers } from './componentPublicInstance'
function setupStatefullComponent(instance){
	const Component = instance.type
+	 instance.proxy = new Proxy({}, PublicInstanceProxyHandlers)
    const { setup } = Component
	if(setup){
		 const setupResult = setup()
		 handleSetupResult(instance, setupResult)
	}
}
```

PublicInstanceProxyHandlers 要获取 instance
```diff
import { PublicInstanceProxyHandlers } from './componentPublicInstance'
function setupStatefulComponent(instance){
	const Component = instance.type
+	instance.proxy = new Proxy({ _: instance }, PublicInstanceProxyHandlers)
	const { setup } = Component
	if(setup){
		const setupResult = setup()
		handleSetupResult(instance, setupResult)
	}
}
```

# 实现组件接收 props

```diff
import { PublicInstanceProxyHandlers } from './componentPublicInstance'
function setupStatefulComponent(instance){
	const Component = instance.type
	instance.proxy = new Proxy({ _: instance}, PublicInstanceProxyHandlers)
	const { setup } = Component
	if(setup){
+		const setupResult = setup(instance.props)
		handleSetupResult(instance, setupResult)
	}
}
```

```diff
import { PublicInstanceProxyHandlers } from './componentPublicInstance'
+ import { shallowReadonly } from '../reactivity/reacitve'
function setupStatefulComponent(instance){
	const Component = instance.type
	instance.proxy = new Proxy({ _: instance}, PublicInstanceProxyHandlers)
	const { setup } = Component
	if(setup){
+		const setupResult = setup(shallowReadonly(instance.props))
		handleSetupResult(instance, setupResult)
	}
}
```

# 实现组件 emit

```diff
import { PublicInstanceProxyHandlers } from './componentPublicInstance'
function setupStatefulComponent(instance){
	const Component = instance.type
	instance.proxy = new Proxy({ _: instance}, PubliceInstanceProxyHandlers)
	const { setup } = Component
	if(setup){
		const setupResult = setup(shallowReadonly(instance.props), {
+			  emit: instance.emit
		})
		handleSetupResult(instance, setupResult)
	}
}
```

# 实现 getCurrentInstance

```diff
+ let currentInstance
import { publicInstanceProxyHandlers } from './componentPublicInstance'
import { shallowReadonly } from '../reactivity/reactive'
function setupStatefulComponent(instance){
	const Component = instance.type
	instance.proxy = new Proxy({_: instance}, publicInstanceProxyHandlers)
	const { setup } = Component
	if(setup){
+		currentInstance = instance 
		const setupResult = setup(shallowReadonly(instance.props), {
			emit: instance.emit
		}) 
+		currentInstance = null
		handleSetupResult(instance, setupResult)
	}
}
```

```diff
import { PublicInstanceProxyHandlers } from './componentPublicInstance'
import { shallowReadonly } from '../reactivity/reactive'
function setupStatefulComponent(instance){
	const Component = instance.type
	instance.proxy = new Proxy({ _: instance}, PubliceInstanceProxyHandlers)
	const { setup } = Component
	if(setup){
+		setCurrentInstance(instance) 
		const setupResult = setup(shallowReadonly(instance.props), {
			  emit: instance.emit
		})
+		setCurrentInstance(null) 
		handleSetupResult(setupResult)
	}
}
```

[[PubliceInstanceProxyHandlers]]
[[setCurrentInstance]]
[[handleSetupResult]]