[[实现 reactive]]
[[实现 readonly]]
```diff
import { track, trigger } from "./effect";

+ function createGetter(isReadonly = false) {
+  return function get(target, key) {
+   const res = Reflect.get(target, key);
+   if (!isReadonly) {
+     track(target, key);
+   }
+   return res;
+  };
+ }

+ function createSetter() {
+  return function set(target, key, value) {
+   const res = Reflect.set(target, key, value);
+   trigger(target, key);
+   return res;
+  };
+ }

export function reactive(raw) {
  return new Proxy(raw, {
+   get: createGetter(),
+   set: createSetter()
}

export function readonly(raw) {
  return new Proxy(raw, {
+   get: createGetter(false),
	set(target, key, value) {
	    console.warn(`can't be set, beacuse ${target} is readonly`);
	    return true;
	},
}
```