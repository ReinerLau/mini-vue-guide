`src/runtime-core/componentSlots.ts`

# 实现组件 slots

```ts
function normalizeObjectSlots(children, slots){
	for(const key in children){
		const value = children[key]
		slots[key] = Array.isArray(value) ? value : [value]
	}
}
```

具名插槽
```diff
function normalizeObjectSlots(children, slots){
	for(const key in children){
		const value = children[key]
+		slots[key] = normalizeSlotValue(value)	
	}
}
```

作用域插槽
```diff
function normalizeObjectSlots(children, slots){
	for(const key in children){
		const value = children[key]
+		slots[key] = (props) => normalizeSlotValue(value(props))
	}
}
```

[[normalizSlotValue#实现组件 slots]]