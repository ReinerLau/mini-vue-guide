作用是对包含 ref 值的对象进行代理，使其每次访问属性时不需要 .value

拦截到访问对象上的属性值时，使用 [[实现 unRef|unRef]] 函数判断该值是否为 ref 值，是则返回 .value 的值，否则直接该值
`src/reactivity/ref.ts`
```diff
export function proxyRefs(objectWithRef){
+	return new Proxy(objectWithRef, {
+		 get(target, key){
+		   return unRef(Reflect.get(target, key))
+		 }
+	})
}

+ export function unRef(ref){
+	return isRef(ref) ? ref.value : ref
+ }
```

拦截到设置对象上的属性值时，使用 [[实现 isRef|isRef]] 判断,如果旧值是 ref 值，新值不是 ref 值，则赋值给旧值的 value 属性, 其余情况直接覆盖旧值
`src/reactivity/ref.ts`
```diff
export function proxyRefs(objectWithRef){
	return new Proxy(objectWithRef, {
+		 set(target, key, value){
+			if(isRef(target[key]) && !isRef(value)) {
+				return (target[key].value = value)
+			}else {
+				return Reflect.set(target, key, value)
+			}
+		 }
	})
}

+ export function isRef(ref){
+	return !!ref.__v_isRef
+ }
```