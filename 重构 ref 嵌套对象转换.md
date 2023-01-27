[[实现 ref 嵌套对象转换]]
```diff
class RefImpl {
  private _value: any;
  private dep = new Set();
  private _rawValue: any;
  constructor(value) {
    this._rawValue = value;
+   this._value = convert(value);
  }

  get value() {
    trackRefValue(this.dep);
    return this._value;
  }

  set value(newValue) {
    if (hasChange(this._rawValue, newValue)) {
      this._rawValue = newValue;
+     this._value = convert(newValue);
      triggerEffects(this.dep);
    }
  }
}

+ function convert(value) {
+  return isObject(value) ? reactive(value) : value;
+ }
```