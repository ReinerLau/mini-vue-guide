`src/runtime-core/helpers.ts`

# 实现组件 slots

```ts
import { createVnode } from './vnode'
export function renderSlots(slots){
	return createVnode('div', {}, slots)	
}
```

`src/runtime-core/index.ts`
```diff
export { createApp } from './createApp'
export { h } from './h'
+ export { renderSlots } from './helpers'
```

具名插槽
```diff
import { createVnode } from './vnode'
+ export function renderSlots(slots, name){
	const slot = slots[name]
+	if(slot){
+		return createVnode('div', {}, slot)
+	}
}
```

作用域插槽
```diff
export function renderSlots(slots, name, props){
	const slot = slots[name]
	if(slot){
		 if(typeof slot === 'function'){
+			return createVnode('div', {}, slot(props)) 
		 }
	}
}
```

[[createVnode]]