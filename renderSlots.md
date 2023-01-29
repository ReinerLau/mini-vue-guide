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

[[createVnode]]