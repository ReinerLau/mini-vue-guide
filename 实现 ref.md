用 class 的目的是因为 proxy 只能处理 object， 不能处理基本数据类型，所以利用 class 的 get 和 set  访问器做和 proxy 相似的处理，收集依赖和触发依赖
```ts
import { trackEffect, triggerEffects, isTracking } from "./effect";

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
	if (Object.is(this._value, newValue)) return;
    this._value = newValue;
    triggerEffects(this.dep);
  }
}

export function ref(value) {
  return new RefImpl(value);
}
```

```ts
export function trackEffect(dep) {
  if (dep.has(activeEffect)) return;

  dep.add(activeEffect);

  activeEffect.deps.push(dep);
}

export function triggerEffects(dep) {
  for (const effect of dep) {
    if (effect.scheduler) {
      effect.scheduler();
    } else {
      effect.run();
    }
  }
}
```

[[优化 effect 的  stop]]
```diff
const targetMap = new Map();

export function track(target, key) {
  if (!isTracking()) return;

  let depsMap = targetMap.get(target);
  if (!depsMap) {
    depsMap = new Map();
    targetMap.set(target, depsMap);
  }
  let dep = depsMap.get(key);
  if (!dep) {
    dep = new Set();
    depsMap.set(key, dep);
  }

+ trackEffect(dep);
}
```

