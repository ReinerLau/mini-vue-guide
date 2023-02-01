`example/update/App.js`
```diff
+ import { h, ref } from '../../lib/mini-vue.esm.js'
export const App = {
	render(){
+		const app = h('p', {}, this.count)
+		const button = h('button', {onClick: this.onClick}, 'button')
		return h('div', {}, [app, button])
	},
	setup(){
+		 const count = ref(1)
		 return {
+			 count,
+			 onClick(){
+				this.count++
+			 }
		 }
	}
}
```

要在 render 中直接访问 ref 值而不需要 .value 则需要使用 [[实现 proxyRefs|proxyRefs]] 函数对包含 ref 值的 setup 返回对象进行代理
`src/runtime-core/component.ts`
```diff
import { proxyRefs } from '../reactivity/ref'
function handleSetupResult(instance, setupResult){
+	instance.setupState = proxyRefs(setupResult)
}
```