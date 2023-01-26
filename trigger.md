# 完整代码

```ts
const targetMaps = new Map()
export function trigger(target, key) {
  let depsMap = targetMaps.get(target);
  let dep = depsMap.get(key);
  for (const effect of dep) {
    effect.run();
  }
}
```

# run

- [[ReactiveEffect#run|run]]