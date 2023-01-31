`example/apiInject/Appjs`
```diff
+ import { h, inject, provide } from '../../lib/mini-vue.esm.js'
export const App = {
	render(){
		 const Consumer = {
			setup(){
+				const foo = inject('foo') 
+				const bar = inject('bar') 
				return {
					foo,
					bar
				}	
			}
			render(){
				return h('p', {}, 'Consumer ' + this.foo + this.bar)
			}
		 }
		 const Provider = {
			 render(){
				const provider = h('p', {}, 'provider')
				return h('div', {}, [provider, h(Consumer)])
			 },
			 setup(){
+				provide('foo', '123')
+				provide('bar', '456')
			 }  
		 }
		 return h('div', {}, [h(Provider)])
	}
}
```

provide 和 inject 的作用是实现跨组件通信

provide 函数接收一个 key 值 和 value 值，然后通过前面实现的 [[实现 getCurrentInstance|getCurrentInstance]]  函数拿到当前组件实例，并保存到组件实例的 provides 属性上，所以 provide 和 inject 只能在 setup 方法中使用
`src/runtime-core/apiInject.ts`
```diff
+ import { getCurrentInstance } from './component'
export function provide(key, val){
+	const currentInstance = getCurrentInstance()
+	const { provides } = currentInstance
+	provides[key] = val
}
```

inject 函数接收一个 key 值，同样通过 getCurrentInstance 函数拿到当前组件实例，但不是从当前组件实例取出 provides 的属性，而是从当前组件实例的父组件实例中取出 provides 属性，因为 provide 的值都是在父组件中保存的
`src/runtime-core/apiInject.ts`
```diff
+import { getCurrentInstance } from './component.ts'
export function inject(key){
+	const currentInstance = getCurrentInstance()	
+	const parentProvides = currentInstance.parent.provides 
+	return parentProvides[key]	
}
```

因为组件间的关系不只有父子关系，还有爷孙等多层级关系，简单实现就是将父组件的 provides 指向更上一层的 provides，但最终获取的结果是以最上级的组件为准, 即如果中间层级的组件提供相同的 key 值会被忽略
`src/runtime-core/component.ts`
```diff
export function createComponentInstance(vnode, parent){
	const component = {
+		 provides: parent ? parent.provides : {} 
		 parent
	}
	return component
}
```

可以利用原型链将 provides 对象的原型指定为上一个层级组件实例的 provides，这样在搜索值时会优先查找最近层级的组件
`src/runtime-core/apiInject.ts`
```diff
import { getCurrentInstance } from './component.ts'
export function provide(key, val){
	const currentInstance = getCurrentInstance()
	let { provides } = currentInstance
    const parentProvides = currentInstance.parent.provides
+	if(provides === parentProvides){
+		 provides = currentInstance.provides = Object.create(parentProvides)
+	}
	provides[key] = val
}
```

最后 inject 还提供一个默认值功能，即找不到对应 key 值时，返回默认值
`src/runtime-core/apiInject.ts`
```diff
import { getCurrentInstance } from './component'
export function inject(key, defaultValue){
	const currentInstance = getCurrentInstance()
	const parentProvides = currentInstance.parent.provides
+	if(key in parentProvides){
		 return parentProvides[key]
+	}else if(defaultValue){
+		 return defaultValue
+	}
}
```