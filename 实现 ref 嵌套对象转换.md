[[重构 ref]]
```diff
+ import { hasChange, isObject } from "../shared";
import { trackEffect, triggerEffects, isTracking } from "./effect";
+ import { reactive } from "./reactive";

class RefImpl {
  private _value: any;
  private dep = new Set();
+ private _rawValue: any;
  constructor(value) {
+   this._rawValue = value;
+   this._value = isObject(value) ? reactive(value) : value;
  }

  get value() {
    trackRefValue(this.dep);
    return this._value;
  }

  set value(newValue) {
    if (hasChange(this._rawValue, newValue)) {
+     this._rawValue = newValue;
+     this._value = isObject(newValue) ? reactive(newValue) : newValue;
      triggerEffects(this.dep);
    }
  }
}
```