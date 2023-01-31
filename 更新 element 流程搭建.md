`example/update/App.js`
```diff
import { h } from '../../lib/mini-vue.esm.js'
export const App = {
	render(){
+		const app = h('p', {}, this.count)
+		const button = h('button', {onClick: this.onClick}, 'button')
		return h('div', {}, [app, button])
	},
	setup(){
		 return {
+			 count: 1,
+			 onClick(){
+				this.count++
+			 }
		 }
	}
}
```