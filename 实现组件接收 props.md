`example/helloworld/foo.js`
```js
import { h } from '../../lib/mini-vue.esm.js'
export const Foo = {
	setup(props){
		console.log(props)
		props.count++
	},
	render(){
		return h('div', {}, 'foo: ' + this.count)
	}
}
```

`example/helloworld/App.js`
```diff
import { h } from '../../lib/mini-vue.esm.js'
+ import { Foo } from './Foo.js'
export const App = {
	render(){
		return h('div', {id: 'root'}, [
			h('div', {}, 'hi,' + this.msg)
+			h(Foo, { count: 1 })
		])
	},
	setup(){
		 return {
			msg: 'mini-vue'
		 }
	}
} 
```

[[setupComponent#实现组件接收 props]]
[[initProps#实现组件接收 props]]
[[createComponentInstance#实现组件接收 props]]
[[setupStatefulComponet#实现组件接收 props]]
[[createReactiveObject#实现组件接收 props]]
[[PubliceInstanceProxyHandlers#实现组件接收 props]]
[[hasOwn#实现组件接收 props]]

