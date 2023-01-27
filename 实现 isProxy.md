```ts
export function isProxy(value) {
  return isReactive(value) || isReadonly(value);
}
```