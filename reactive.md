### 完整代码

作用是创建响应式对象，监听响应式对象的操作触发自动更新
```ts
import { track, trigger } from "./effect";

export function reactive(raw) {
  return new Proxy(raw, {
    get(target, key) {
      const res = Reflect.get(target, key);
      track(target, key);
      return res;
    },
    set(target, key, value) {
      const res = Reflect.set(target, key, value);
      trigger(target, key);
      return res;
    },
  });
}
```

### 创建代理对象

原理是创建 Proxy 代理对象，拦截对象的各种操作进行特殊处理
```diff
export function reactive(raw) {
+  return new Proxy(raw, {
+     // ......
+  });
}
```

### get

访问属性时拦截 get 操作，先是使用 Reflect 重建 get 操作获取属性值，然后使用 [[track]] 收集依赖
```diff
export function reactive(raw) {
  return new Proxy(raw, {
+   get(target, key) {
+     const res = Reflect.get(target, key);
+     track(target, key);
+     return res;
+   }
  });
}
```
