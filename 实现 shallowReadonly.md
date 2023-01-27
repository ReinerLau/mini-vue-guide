```ts
// reactive.ts
import {
  mutableHandlers,
  readonlyHandlers,
  shallowReadonlyHandlers,
} from "./baseHandlers";

export function shallowReadonly(raw) {
  return createReactiveObject(raw, shallowReadonlyHandlers);
}
```

[[实现 isReadonly]]
```diff
+ import { extend, isObject } from "../shared";

+ function createGetter(isReadonly = false, shallow = false) {
  return function get(target, key) {
    if (key === ReactiveFlags.IS_REACTIVE) {
      return !isReadonly;
    } else if (key === ReactiveFlags.IS_READONLY) {
      return isReadonly;
    }

    const res = Reflect.get(target, key);

+   if (shallow) {
+     return res;
+   }

    if (isObject(res)) {
      return isReadonly ? readonly(res) : reactive(res);
    }

    if (!isReadonly) {
      track(target, key);
    }
    return res;
  };
}

+ const shallowReadonlyGet = createGetter(true, true);

export const readonlyHandlers = {
  get: readonlyGet,
  set(target, key, value) {
    console.warn(`can't be set, beacuse ${target} is readonly`);
    return true;
  },
};

+ export const shallowReadonlyHandlers = extend({}, readonlyHandlers, {
+   get: shallowReadonlyGet,
+ });
```