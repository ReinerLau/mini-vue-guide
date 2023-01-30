`src/runtime-core/renderer.ts`

初始化 component
```ts
function patch(vnode, container) {
  processComponent(vnode, container);
}
```

初始化 element
```diff
+ import { isObject } from '../shared/index'
function patch(vnode, container) {
+ if (typeof vnode.type === "string") {
+   processElement(vnode, container);
+ } else if (isObject(vnode.type)) {
    processComponent(vnode, container);
+ }
}
```

# 实现 shapFlags

```diff
+ import { ShapFlags } from '../shared/ShapFlags'
function patch(vnode, container){
+	if(vnode.shapFlag & ShapFlgs.ELEMENT){
		 processElement(vnode, container)
+	}else if(vnode.shapFlag & ShapFlags.STATEFUL_COMPONENT){
		 processComponent(vnode, container)
	}
}
```

# 实现 Fragment

```diff
import { ShapFlags } from '../shared/ShapFlags'
function patch(vnode, container){
+	const { type, shapFlag } = vnode
+	switch(type){
+		case 'Fragment':
+			processsFragment(vnode, container)
+			break
+		default:
			if(shapFlag & ShapFlags.ELEMENT){
				 processElement(vnode, container)
			}else if(shapFlag & ShapFlags.STATEFUL_COMPONENT){
				 processComponent(vnode, container)
			}
+	}
}
```

[[processFragment]]
[[processElement]]
[[processComponent]]