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

当 render 中的 ref 值更新后需要重新渲染则可以将渲染组件的过程视为依赖使用[[实现 effect|effect]]进行收集，当 ref 值更新后触发渲染组件
`src/runtime-core/component.ts`
```diff
+ import { effect } from '../reactivity/effect'
function setupRenderEffect(instance, container){
+	effect(() => {
		const { proxy } = instance
		const subTree = instance.render.call(proxy)
		patch(subTree, container)
+	})    
}
```

使用组件实例上的 isMounted 标记区分初始化和更新
`src/runtime-core/renderer.ts`
```diff
import { effect } from '../reactivity/effect'
function setupRenderEffect(instance, container){
	effect(() => {
+		 if(!instance.isMounted){
			const { proxy } = instance
			const subTree = instance.render.call(proxy)
			patch(subTree, container)
+			instance.isMounted = true
+		 }else{
+			console.log('update')
+		 }
	})
}
```

`src/runtime-core/component.ts`
```diff
export function createComponentInstance(vnode){
	return {
+		 isMounted: false
	}
}
```

加载
