`example/helloworld/App.js`
```diff
import { h } from '../../lib/mini-vue.esm.js'
import { Foo } from './Foo.js'
export const App = {
	render(){
		const app = h('p', {}, 'app')
		const foo = h(Foo, { onAdd: this.onAddEmit, onAddFoo: this.onAddFoo })
+		return h('div', {}, [app, foo])
	},
	setup(){
		return {
+			onAddEmit(a, b){
+				console.log('onAdd', a, b)
+			},
+			onAddFoo(){
+			   console.log('onAddFoo')
+			}
		}
	}
}
```

`example/helloworld/Foo.js`
```diff
import { h } from '../../lib/mini-vue.esm.js'
export const Foo = {
	render(){
+		const button = h('button', { onClick: this.onClick}, 'button')
		const foo = h('p', {}, 'foo')
		return h('div', {}, [foo, button])
	},
+	setup(props, {emit}){
		 return {
		   onClick(){
+			 emit('add', 1, 2)
+			 emit('add-foo')
		   }
		 }
	}
}
```

[[setupStatefulComponet#实现组件 emit]]
[[emit#实现组件 emit]]
[[createComponentInstance#实现组件 emit]]
