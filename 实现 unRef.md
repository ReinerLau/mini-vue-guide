使用[[实现 isRef|isRef]]判断是否为 ref 值再决定是否返回 .value，还是直接返回
```ts
export function unRef(ref) {
  return isRef(ref) ? ref.value : ref;
}
```