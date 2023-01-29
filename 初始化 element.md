children 是字符串的情况
`example/helloworld/App.js`
```js
import { h } from '../../lib/mini-vue.esm.js'
export default App = {
	render(){
		return h('div', {id: 'root'}, 'hi ' + this.msg)
	},
	setup(){
		return {
			msg: 'mini-vue'
		}
	}
}
```

children 是数组的情况
`example/helloworld/App.js
```js
import { h } from '../../lib/mini-vue.esm.js'
export default App = {
	render(){
		return h('div', {id: 'root'}, [
			h('div', {class: 'blue'}, 'hi'),
			h('div', {class: 'red'}, 'mini-vue')
		])
	}
}
```

[[createApp]]