[[实现 ref]]
[[重构 ref]]
[[实现 ref 嵌套对象转换]]
[[重构 ref 嵌套对象转换]]
```ts
import { effect } from "../effect";
import { ref } from "../ref";

describe("ref", () => {
  it("happy path", () => {
    const foo = ref(1);
    expect(foo.value).toBe(1);
  });

  it("should be reactive", () => {
    const foo = ref(1);
    let dummy;
    let call = 0;
    effect(() => {
	  call++
      dummy = foo.value;
    });

    expect(dummy).toBe(1);
    foo.value = 2;
    expect(foo.value).toBe(2);
    expect(dummy).toBe(2);
    expect(call).toBe(2);

	foo.value = 2
	expect(call).toBe(2)
  });

  it("nested should be reactive", () => {
    const foo = ref({
      count: 1,
    });
    let dummy;
    effect(() => {
      dummy = foo.value.count;
    });
    expect(dummy).toBe(1);
    foo.value.count++;
    expect(dummy).toBe(2);
  });
});
```