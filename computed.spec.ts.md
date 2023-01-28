[[实现 computed]]
```ts
import { computed } from "../computed";
import { reactive } from "../reactive";

describe("computed", () => {
  it("happy path", () => {
    const user = reactive({
      age: 18,
    });

    const age = computed(() => {
      return user.age;
    });

    expect(age.value).toBe(18);
  });

  it("should compute lazily", () => {
    const obj = reactive({
      foo: 1,
    });

    const getter = jest.fn(() => {
      return obj.foo;
    });

    const cValue = computed(getter);

    expect(getter).not.toHaveBeenCalled();

    cValue.value;
    expect(getter).toHaveBeenCalledTimes(1);

    cValue.value;
    expect(getter).toHaveBeenCalledTimes(1);

    obj.foo = 2;
    expect(getter).toHaveBeenCalledTimes(1);
    expect(cValue.value).toBe(2);
    expect(getter).toHaveBeenCalledTimes(2);

    cValue.value;
    expect(getter).toHaveBeenCalledTimes(2);
  });
});
```