元素或组件对象转换为 vnode
```ts
export function createVnode(type, props?, children?) {
  const vnode = {
    type,
    props,
    children,
  };
  return vnode;
}
```

# 实现组件代理对象

保存根节点元素
```diff
export function createVnode(type, props?, children?){
	const vnode = {
		 type,
		 props,
		 children,
+		 el: null
	}
	return vnode
}
```

# 实现 shapFlags

先获取根节点的类型
```diff
+ import { ShapFlags } from '../shared/ShapFlags'
export function createVnode(type, props?, children?){
+	 const vnode = {
		type,
		props,
		children,
+		shapFlags: getShapFlag(type)
		el: null
	}
+	 if(typeof children === 'string'){
+		  vnode.shapFlag |= ShapFlags.TEXT_CHILDREN
+	 }else if(Array.isArray(children)){
+		  vnode.shapFlag |= ShapFlags.ARRAY_CHILDREN
+	 }
+	return vnode
}
```

# 实现组件 slots

```diff
import { ShapFlags } from '../shared/ShapFlags'
export function createVnode(type, props?, children?){
	const vnode = {
		type,
		props,
		children,
		shapFlags: getShapFlag(type)
		el: null
	}
	 if(typeof children === 'string'){
		vnode.shapFlags |= ShapFlags.TEXT_CHILDREN
	 }else if(Array.isArray(children)){
		vnode.shapFlags |= ShapFlags.ARRAY_CHILDREN
	 }

+	if(vnode.type & ShapFlags.STATEFUL_COMPONENT){
+		 if(typeof children === 'object'){
+			  vnode.shapFlags |= ShapFlags.SLOT_CHILDREN
+		 }
+	}
	return vnode
}
```