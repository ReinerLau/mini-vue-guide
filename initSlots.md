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