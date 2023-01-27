[[实现 isReactive]]
```diff
+ export const enum ReactiveFlags {
+  IS_REACTIVE = "__v_isReactive",
+ }

export function isReactive(value) {
+ return !!value[ReactiveFlags.IS_REACTIVE];
}
```

```diff
+ import { ReactiveFlags } from "./reactive";

function createGetter(isReadonly = false) {
  return function get(target, key) {
+  if (key === ReactiveFlags.IS_REACTIVE) {
      return !isReadonly;
    }

    const res = Reflect.get(target, key);
    if (!isReadonly) {
      track(target, key);
    }
    return res;
  };
}
```