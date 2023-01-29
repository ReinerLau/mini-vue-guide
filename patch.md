初始化 component
```ts
function patch(vnode, container) {
  processComponent(vnode, container);
}
```
[[processComponent]]

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
[[processElement]]