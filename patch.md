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

[[processElement]]
[[processComponent]]