父组件向子组件传一个虚拟节点
`example/helloworld/App.js`
```diff
import { h } from '../../lib/mini-vue.esm.js'
+ import { Foo } from './Foo.js'
export const App = {
	render(){
		 const app = h('div', {}, 'hi,' + this.msg)
+		 const foo = h(Foo, {}, h('p', {}, '123'))
+		 return h('div', {}, [app, foo])
	},
	setup(){
		 return {
		   msg: 'mini-vue'
		 }
	}
}
```

子组件用 this.$slots 接收父组件传过来的虚拟节点
`example/hellowordl/Foo.js`
```diff
import { h } from '../../lib/mini-vue.esm.js'
export const Foo = {
	render(){
		const foo = h('p', {}, 'foo')
+		return h('div', {}, [foo, this.$slots])
	}
}
```

[[setupComponent#实现组件 slots]]
[[initSlots#实现组件 slots]]
[[PubliceInstanceProxyHandlers#实现组件 slots]]