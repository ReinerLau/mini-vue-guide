[[实现 shallowReadonly]]
```ts
import { isReadonly, shallowReadonly } from "../reactive";

describe("shallowReadonly", () => {
  it("happy path", () => {
    const obj = shallowReadonly({ foo: { bar: 1 } });
    expect(isReadonly(obj)).toBe(true);
    expect(isReadonly(obj.foo)).toBe(false);
  });

  it("should call console.warn when set", () => {
    const observed = shallowReadonly({ foo: 1 });
    console.warn = jest.fn();
    observed.foo = 2;
    expect(console.warn).toHaveBeenCalled();
  });
});
```