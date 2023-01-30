获取当前组件实例

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

[[getCurrentInstance#实现 getCurrentInstance]]
[[setupStatefulComponet#实现 getCurrentInstance]]
[[setCurrentInstance#实现 getCurrentInstance]]