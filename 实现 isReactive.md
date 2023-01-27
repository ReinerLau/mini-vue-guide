```ts
export function isReactive(value) {
  return !!value["is_reactive"];
}
```

[[重构 baseHandler]]
```diff
function createGetter(isReadonly = false) {
  return function get(target, key) {
+   if (key === "is_reactive") {
+     return !isReadonly;
+   }

    const res = Reflect.get(target, key);
    if (!isReadonly) {
      track(target, key);
    }
    return res;
  };
}
```