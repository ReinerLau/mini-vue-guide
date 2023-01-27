[[实现 reactive]]
[[实现 isReactive]]
[[重构 isReactive]]
[[实现嵌套对象转换]]
```ts
import { reactive, isReactive } from "../reactive";

describe("reactive", () => {
  it("happy path", () => {
    const orignal = { foo: 1, bar: { foo: 1 } };
    const observed = reactive(orignal);
    expect(observed).not.toBe(orignal);
    expect(observed.foo).toBe(1);
    expect(isReactive(observed)).toBe(true);
    expect(isReactive(orignal)).toBe(false);
    expect(isReactive(observed.bar)).toBe(true);
    expect(isReactive(orignal.bar)).toBe(false);
  });
});
```