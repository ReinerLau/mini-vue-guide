`src/runtime-core/component.ts`

# 实现 getCurrentInstance

```ts
let currentInstance
export function getCurrentInstance(){
	return currentInstance
}
```

`src/runtime-core/index.ts`
```ts
export { getCurrentInstance } from './component'
```