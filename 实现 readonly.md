```ts
export function readonly(raw) {
  return new Proxy(raw, {
    get(target, key) {
      const res = Reflect.get(target, key);
      return res;
    },
    set(target, key, value) {
      console.warn(
        `key :"${String(key)}" set 失败，因为 target 是 readonly 类型`,
        target
      );
      return true;
    },
  });
}
```