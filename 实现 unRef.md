```ts
export function unRef(ref) {
  return isRef(ref) ? ref.value : ref;
}
```