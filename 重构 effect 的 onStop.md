[[实现 effect 的 onStop]]
```diff
+ import { extend } from "../shared";

export function effect(fn, options: any = {}) {
  const _effect = new ReactiveEffect(fn, options.scheduler);
+ extend(_effect, options);

  _effect.run();

  const runner: any = _effect.run.bind(_effect);
  runner._effect = _effect;

  return runner;
}
```

封装成工具函数
```ts
export const extend = Object.assign;
```