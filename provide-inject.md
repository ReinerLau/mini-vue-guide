`src/runtime-core/apiInject.ts`

```ts
export function provide(){}
export function inject(){}
```

`src/runtime-core/index.ts`
```ts
export * from './apiInject'
```

```diff
+ import { getCurrentInstance } from './component'
+ export function provide(key, val){
+	const currentInstance = getCurrentInstance()
+	if(currentInstance){
+		const { provides } = instance
+		provide[key] = val
+	}
}
```