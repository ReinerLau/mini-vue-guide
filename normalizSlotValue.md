`src/runtime-core/componentSlot.ts`

# 实现组件 slots

```ts
function normalizeSlotValue(value){
	return Array.isArray(value) ? value : [value]
}
```