
`example/helloworld/App.js`
```diff
+ import { h, getCurrentInstance } from '../../lib/mini-vue.esm.js'
import { Foo } from './Foo.js'
export const App = {
	render(){
		const app = h('p', {}, 'app')
		const foo = h(Foo)
		return h('div', {}, [app, foo])
	},
	setup(){
+		const app = getCurrentInstance() 
+		console.log(app) 
	}
}
```

`example/hellowordl/Foo.js`
```diff
+ import { h, getCurrentInstance } from '../../lib/mini-vue.esm.js'
export const Foo = {
	render(){
		 return h('p', {}, 'foo')
	},
	setup(){
+		const foo = getCurrentInstance() 
+		console.log(foo)
	}
}
```

作用是获取当前组件实例

只能在当前组件的 setup 方法中调用，因为是在初始化 setup 返回结果时，也就是创建组件实例之后才能获取组件实例
`src/runtime-core/component.ts`
```diff
+ let currentInstance
export function setupStatefulComponent(instance){
	const Component = instance.type
	const { setup } = Component		
	if(setup){
+		 currentInstance = instance
		 const setupResult = setup()
+		 currentInstance = null
		 handleSetupResult(instance, setupResult)
	}
}

+ export function getCurrentInstance(){
+	return currentInstance
+ }
```

通过全局变量保存当前组件实例，调用组件 setup 过程中如果调用了 getCurrentInstance 函数则将该全局变量返回获取组件实例