`src/runtime-core/componentSlots.ts`

# 实现组件 slots

```ts
export function initSlots(instance, children){
	instance.slots = children
}
```