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

从父组件中获取 proivde 的属性
```diff
+ import { getCurrentInstance } from './component'
+ export function inject(key){
+	const currentInstance = getCurrentInstance()	
+	if(currentInstance){
+		const parentProvides = currentInstance.parent.provides
+		return parentProvides[key]
+	}
}
```