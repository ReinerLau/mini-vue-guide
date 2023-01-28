[[实现 computed]]
```diff
class ComputedRefImpl {
  private _getter: any;
+ private _dirty: any = true;
+ private _value: any;
  constructor(getter) {
    this._getter = getter;
  }

  get value() {
+   if (this._dirty) {
+     this._dirty = false;
+     this._value = this._getter();
+   }
+   return this._value;
  }
}
```

[[实现 computed 重新计算]]