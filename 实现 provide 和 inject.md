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
	if(currentInstance){
+		 const { provides } = currentInstance
+		 provides[key] = val
	}
}
```

inject 函数接收一个 key 值，同样通过 getCurrentInstance 函数拿到当前组件实例，但不是从当前组件实例取出 provides 的属性，而是从当前组件实例的父组件实例中取出 provides 属性，因为 provide 的值都是在父组件中保存的

[[provide-inject]]
[[createComponentInstance#实现 provide 和 inject]]