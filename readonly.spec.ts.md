[[实现 readonly]]
[[重构 reative 和 readonly]]
[[实现 baseHandler]]
[[重构 baseHandler]]
[[实现 createReactiveObject]]
```ts
import { readonly } from "../reactive";

describe("readonly", () => {
  it("happy path", () => {
    const original = { foo: 1 };
    const observed = readonly(original);

    expect(observed).not.toBe(original);
    expect(observed.foo).toBe(1);
  });

  it("should call console.warn when set", () => {
    const observed = readonly({ foo: 1 });
    console.warn = jest.fn();
    observed.foo = 2;
    expect(console.warn).toHaveBeenCalled();
  });
});
```