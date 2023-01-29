父组件向子组件传一个虚拟节点
`example/helloworld/App.js`
```diff
import { h } from '../../lib/mini-vue.esm.js'
+ import { Foo } from './Foo.js'
export const App = {
	render(){
		 const app = h('p', {}, 'app')
+		 const foo = h(Foo, {}, h('p', {}, '123'))
+		 return h('div', {}, [app, foo])
	},
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

还要支持数组形式的 slots
`example/helloworld/App.js`
```diff
import { h } from '../../lib/mini-vue.esm.js'
import { Foo } from './Foo.js'
export const App = {
	render(){
		const app = h('p', {}, 'app')
+		const foo = h(Foo, {}, [h('p', {}, '123'), h('p', {}, '456')])
		return h('div', {}, [app, foo])
	}
}
```

`example/helloworld/Foo.js`
```diff
import { h, renderSlots } from '../../lib/mini-vue.esm.js'
export const Foo = {
	render(){
		const foo = h('p', {}, 'foo')
+		return h('div', {}, [foo, renderSlots(this.$slots)])	
	}
}
```

[[setupComponent#实现组件 slots]]
[[initSlots#实现组件 slots]]
[[PubliceInstanceProxyHandlers#实现组件 slots]]
[[renderSlots#实现组件 slots]]