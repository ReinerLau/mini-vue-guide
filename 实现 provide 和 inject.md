实现跨组件通信

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

[[provide-inject]]