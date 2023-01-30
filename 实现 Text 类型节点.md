`examle/helloworld/App.js`
```diff
+ import { h, createTextVNode } from '../../lib/mini-vue.esm.js'
import { Foo } from './Foo.js'
export const App = {
	render(){
		const app = h('p', {}, 'app')
+		const foo = h(Foo, {}, [h('p', {}, '123'), 'test'])
		return h('div', {}, [app, foo])
	}
}
```

[[createTextVNode#实现 Text 类型节点]]
[[Text#实现 Text 类型节点]]
[[patch#实现 Text 类型节点]]
[[processText#实现 Text 类型节点]]