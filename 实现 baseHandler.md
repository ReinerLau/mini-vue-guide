```ts
import { track, trigger } from "./effect";

function createGetter(isReadonly = false) {
  return function get(target, key) {
    const res = Reflect.get(target, key);
    if (!isReadonly) {
      track(target, key);
    }
    return res;
  };
}

function createSetter() {
  return function set(target, key, value) {
    const res = Reflect.set(target, key, value);
    trigger(target, key);
    return res;
  };
}

export const mutableHandlers = {
  get: createGetter(),
  set: createSetter(),
};

export const readonlyHandlers = {
  get: createGetter(true),
  set(target, key, value) {
    console.warn(`can't be set, beacuse ${target} is readonly`);
    return true;
  },
};
```

[[重构 reative 和 readonly]]
```diff
+ import { mutableHandlers, readonlyHandlers } from "./baseHandlers";

export function reactive(raw) {
+ return new Proxy(raw, mutableHandlers);
}

export function readonly(raw) {
+ return new Proxy(raw, readonlyHandlers);
}
```