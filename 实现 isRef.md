利用 ref 值的一个标记变量

`src/reactivity/ref.ts`
```ts
export function isRef(val) {
  return !!val.__v_isRef;
}
```

`src/reactivity/ref.ts`
```diff
class RefImpl {
+ public __v_isRef = true;
}
```