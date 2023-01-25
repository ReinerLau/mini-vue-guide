### 完整代码

```ts
let activeEffect;
const targetMaps = new Map();
export function track(target, key) {
  let depsMap = targetMaps.get(target);
  if (!depsMap) {
    depsMap = new Map();
    targetMaps.set(target, depsMap);
  }
  let dep = depsMap.get(key);
  if (!dep) {
    dep = new Set();
    depsMap.set(key, dep);
  }
  dep.add(activeEffect);
}
```

每次触发响应式对象的 get 操作就会将对应的 effect 实例放进响应式对象对应属性的依赖容器中，结合 Map 和 Set，一个响应式对象对应一个所有属性的依赖 Map，一个属性对应一个依赖 Set
```diff
+ const targetMaps = new Map();
export function track(target, key) {
+  let depsMap = targetMaps.get(target);
+  let dep = depsMap.get(key);
}
```

activeEffect 保存了当前执行的依赖，收集到依赖容器中
```diff
+ let activeEffect;
const targetMaps = new Map();
export function track(target, key) {
  let depsMap = targetMaps.get(target);
  let dep = depsMap.get(key);
+  dep.add(activeEffect);
}
```

要注意首次收集依赖时的初始化问题
```diff
let activeEffect;
const targetMaps = new Map();
export function track(target, key) {
  let depsMap = targetMaps.get(target);
+  if (!depsMap) {
+    depsMap = new Map();
+    targetMaps.set(target, depsMap);
+  }
  let dep = depsMap.get(key);
+  if (!dep) {
+    dep = new Set();
+    depsMap.set(key, dep);
+  }
  dep.add(activeEffect);
}
```