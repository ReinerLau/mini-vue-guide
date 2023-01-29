`src/runtime-core/componentSlots.ts`

# 实现组件 slots

```ts
export function initSlots(instance, children){
	instance.slots = children
}
```

支持组件 slots
```diff
export function initSlots(instance, children){
+	instance.slots = Array.isArray(children) ? children : [children]
}
```

具名插槽
```diff
export function initSlots(instance, children){
+	const slots = {}
+	for(const key in children){
+		const slot = childern[key] 
+		slots[key] = Array.isArray(children) ? children : [children] 
+	}
+	instance.slots = slots
}
```

```diff
export function initSlots(instance, children){
+	normalizeObjectSlots(children, instance.slots)
}
```

```diff
+ import { ShapFlags } from '../shared/ShapFlags'
export function initSlots(instance, children){
+	const { vnode } = instance
+	if(vnode.shapFlag & ShapFlag.SLOT_CHILDREN){
		normalizeObjectSlots(children, instance.slots)
+	}
}
```

[[normalizeObjectSlots#实现组件 slots]]
