创建一个假元素插入到文档中看看效果
`src/runtime-core/renderer.ts`
```ts
function mountElement(vnode, container) {
	const el = document.createElement('div')	
	el.textContent = 'hi mini-vue'
	el.setAttribute('id', 'root')
	document.body.append(el)
}
```

动态创建元素
```diff
function mountElement(vnode, container){
+	const el = document.createElement(vnode.type)
	el.textContent = 'hi, mini-vue'
	el.setAttributes'id', 'root')
	document.body.append(el)
}
```

设置文本 children
```diff
function mountElement(vnode, container){
	const el = document.createElement(vnode.type)
+	const { children } = vnode
+	el.textContent = children
	el.setAttribute('id', 'root')
	document.body.append(el)
}
```

设置数组 children
```diff
function mountElement(vnode, container){
	const el = document.createElement(vnode.type)
	const { children } = vnode
+	if(typeof children === 'string'){
		el.textContent = children
+	}else if(Array.isArray(children)){
+		mountChildren(vnode, el)
+	}
	el.setAttribute('id', 'root')
	document.body.append(el)
}
```
[[mountChildren]]

设置 props
```diff
function mountElement(vnode, container){
	const el = document.createElement(vnode.type)
	const { children } = vnode
	if(typeof children === 'string'){
		el.textContent = children
	}else if(Array.isArray(children)){
		mountChildren(vnode, el)
	}
	const { props } = vnode
+	for(const key in props){
+		const val = props(key)
+		el.setAttribute(key, val)
+	}
	document.body.append(el)
}
```

插入元素
```diff
function mountElement(vnode, container){
	const el = document.createElement(vnode.type)
	const { children } = vnode
	if(typeof children === 'string'){
		el.textContent = children
	}else if(Array.isArray(children)){
		mountChildren(vnode, el)
	}
	for(const key in props){
		const val = props[key]
		el.setAttribute(key, val)
	}
+	container.append(el)
}
```

# 实现组件代理对象

保存根节点的元素
```diff
function mountElement(vnode, container){
+	const el = (vnode.el = document.createElement(vnode.type))
	const { children } = vnode
	if(typeof children === 'string'){
		 el.textContent = children
	}else if(Array.isArray(children)){
		 mountChildren(vnode, container)
	}
	const { props } = vnode 
	for(const key in props){
		const val = props[key]
		el.setAttribute(key, val)
	}
	container.append(el)
}
```

# 实现 shapFlags

```diff
+ import { ShapFlags } from '../shared/ShapFlags'
function mountElement(vnode, container){
	const el = (vnode.el = document.createElement(vnode.type))
	const { children } = vnode
+	if(vnode.shapFlag & ShapFlags.TEXT_CHILDREN){
		 el.textContent = children
+	}else if(vnode.shapFlag & ShapFlags.ARRAY_CHILDREN){
		 mountChildren(vnode, el)
	}
	const { props } = vnode
	for(const key in props){
		const val = props[key]
		el.setAttribue(key, val)
	} 
	container.append(el)
}
```

# 实现注册事件

先写死一个点击事件
```diff
import { ShapFlags } from '../shared/ShapFlags'
function mountElement(vnode, container){
	const el = (vnode.el = document.createElement(vnode.type))
	const { children } = vnode
	if(vnode.shapFlag & ShapFlags.TEXT_CHILDREN){
		 el.textContent = children
	}else if(vnode.shapFlag & ShapFlags.ARRAY_CHILDREN){
		 mountChildren(vnode, el)
	}
	const { props } = vnode
	for(key in props){
		const val = props[key]
+		if(key === 'onClick'){
+			el.addEventListener("click", val)
+		}else {
			el.setAttribute(key, val)  
+		}
	}
}
```

事件改成通用匹配
```diff
import { ShapFlags } from '../../lib/mini-vue.esm.js'
function mountElement(vnode, container){
	const el = (vnode.el = document.createElement(vnode.type))
	const { children } = vnode
	if(vnode.shapFlag & ShapFlags.TEXT_CHILDREN){
		 el.textContent = children
	}else if(vnode.shapFlag & ShapFlags.ARRAY_CHILDREN){
		 mountChildren(vnode, el)
	}
	const { props } = vnode
	for(const key in props){
		const val = props[key]
+		const isOn = (key) => /^on[A-Z]/.test(key)
+		if(isOn(key)){
+			const event = key.slice(2).toLocateLowerCase()
+			el.addEvenetListener(event, val)
		}else {
			el.setAttribute(key, val)
		}
	}
}
```