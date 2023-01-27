[[重构 isReactive]]
```diff
export const enum ReactiveFlags {
  IS_REACTIVE = "__v_isReactive",
+ IS_READONLY = "__v_isReadonly",
}

+ export function isReadonly(value) {
+  return !!value[ReactiveFlags.IS_READONLY];
+ }
```

```diff
import { track, trigger } from "./effect";
import { ReactiveFlags } from "./reactive";

function createGetter(isReadonly = false) {
  return function get(target, key) {
    if (key === ReactiveFlags.IS_REACTIVE) {
      return !isReadonly;
+   } else if (key === ReactiveFlags.IS_READONLY) {
+     return isReadonly;
+   }

    const res = Reflect.get(target, key);
    if (!isReadonly) {
      track(target, key);
    }
    return res;
  };
}
```