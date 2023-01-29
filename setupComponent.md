`src/runtime-core/component.ts`

初始化组件
```ts
export function setupComponent(instance) {
  setupStatefulComponent(instance);
}
```

# 实现组件接收 props

```diff
+ import { initProps } from '../componentProps'
export function setupComponent(instance){
+	initProps(instance, instance.vnode.props)
	setupStatefulComponent(instance)
}
```

# 实现组件 slots

```diff
import { initProps } from './componentProps'
+ import { initSlots } from './componentSlots'
export function setupComponet(instance){
	initProps(instance, instance.vnode.props)
+	initSlots(instance, instance.vnode.children)
	setupStatefulComponent(instance)
}
```

[[initProps]]
[[initSlots]]
[[setupStatefulComponet]]