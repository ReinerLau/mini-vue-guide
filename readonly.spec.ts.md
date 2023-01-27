[[实现 readonly]]
[[重构 reative 和 readonly]]
[[实现 baseHandler]]
[[重构 baseHandler]]
[[实现 createReactiveObject]]
[[实现 isReadonly]]
[[实现嵌套对象转换]]
[[实现 isProxy]]
```ts
import { readonly, isReadonly, isProxy } from "../reactive";

describe("readonly", () => {
  it("happy path", () => {
    const original = { foo: 1, bar: { foo: 1 } };
    const observed = readonly(original);

    expect(observed).not.toBe(original);
    expect(observed.foo).toBe(1);
	expect(isReadonly(observed)).toBe(true);
    expect(isReadonly(original)).toBe(false);
    expect(isReadonly(observed.bar)).toBe(true);
    expect(isReadonly(original.bar)).toBe(false);
    expect(isProxy(observed)).toBe(true);
  });

  it("should call console.warn when set", () => {
    const observed = readonly({ foo: 1 });
    console.warn = jest.fn();
    observed.foo = 2;
    expect(console.warn).toHaveBeenCalled();
  });
});
```