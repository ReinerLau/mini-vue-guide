其创建的实例将作为依赖被收集和触发
```ts
class ReactiveEffect {
  private _fn: any;

  constructor(fn) {
    this._fn = fn;
  }

  run() {
    activeEffect = this;
    this._fn();
  }
}
```

接收的函数作为私有属性，开头使用下划线和 private 标记
```diff
class ReactiveEffect {
+ private _fn;
}
```

run 方法在触发依赖回调时使用，回调中通常包含触发响应式对象的 [[reactive#proxy.get|get]] 操作而产生一些副作用
```diff
class ReactiveEffect {
+ run() {
+   this._fn();
+ }
}
```

activeEffect 用于保存当前正在执行的依赖，用于收集依赖
```diff
class ReactiveEffect {
	run(){
+		activeEffect = this
		this._fn()_
	}
}
```