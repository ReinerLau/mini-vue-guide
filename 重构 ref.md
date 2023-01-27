[[实现 ref]]
```diff
+ import { hasChange } from "../shared";

class RefImpl {
  private _value: any;
  private dep = new Set();
  constructor(value) {
    this._value = value;
  }

  get value() {
    if (isTracking()) {
      trackEffect(this.dep);
    }
    return this._value;
  }

  set value(newValue) {
+   if (hasChange(this._value, newValue)) {
      this._value = newValue;
      triggerEffects(this.dep);
+   }
  }
}
```

```ts
export function hasChange(oldValue, newValue) {
  return !Object.is(oldValue, newValue);
}
```

```diff
class RefImpl {
  private _value: any;
  private dep = new Set();
  constructor(value) {
    this._value = value;
  }

  get value() {
+   trackRefValue(this.dep);
    return this._value;
  }

  set value(newValue) {
    if (hasChange(this._value, newValue)) {
      this._value = newValue;
      triggerEffects(this.dep);
    }
  }
}

+ function trackRefValue(dep) {
+  if (isTracking()) {
+   trackEffect(dep);
+  }
+ }
```