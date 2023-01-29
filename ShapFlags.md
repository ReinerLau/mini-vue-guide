`src/shared/ShapFlags.ts`

# 实现 shapFlags

<< 代表向左移动多少位
```ts
export const enum ShapFlags {
	ELEMENT = 1,
	STATEFUL_COMPONENT = 1 << 1,
	TEXT_CHILDREN = 1 << 2,
	ARRAY_CHILDREN = 1 << 3
}
```

# 实现组件 slots

```diff
export const enum ShapFlags {
	ELEMENT = 1,
	STATEFUL_COMPONENT = 1 << 1,
	TEXT_CHILDREN = 1 << 2,
	ARRAY_CHILDREN = 1 << 3,
+	SLOT_CHILDREN = 1 << 4
}
```