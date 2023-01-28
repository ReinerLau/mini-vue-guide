组件对象的 render 方法必须返回 vnode，h 其实就是 [[createVnode]] 的别名
`example/helloworld/App.js`
```diff
+ import { h } from '../../lib/mini-vue.esm.js'
export default App = {
	render(){
+		return h('div', {}, 'hi' + this.msg)
	},
	setup(){
		return {
			msg: 'mini-vue'
		}
	}
}
```

runtime-core 模块导出 h
`src/runtime-core/index.ts`
```diff
export { createApp } from './createApp'
+ export { h } from './h'
```

`src/runtime-core/h.ts`
```ts
import { createVnode } from './vnode'
export function h(type, props?, children?){
	return createVnode(type, props, children)
}
```
[[createVnode]]