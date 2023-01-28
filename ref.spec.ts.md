[[实现 ref]]
[[重构 ref]]
[[实现 ref 嵌套对象转换]]
[[重构 ref 嵌套对象转换]]
[[实现 isRef]]
[[实现 unRef]]
[[实现 proxyRefs]]
```ts
import { effect } from "../effect";
import { ref, isRef, unRef, proxyRefs } from "../ref";

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

  it("isRef", () => {
    const foo = ref(1);
    const user = reactive({
      foo: 1,
    });

    expect(isRef(foo)).toBe(true);
    expect(isRef(1)).toBe(false);
    expect(isRef(user)).toBe(false);
  });

  it("unRef", () => {
    const foo = ref(1);
    expect(unRef(foo)).toBe(1);
    expect(unRef(1)).toBe(1);
  });

  it("proxyRefs", () => {
    const user = {
      age: ref(18),
      name: "Reiner",
    };

    const proxyUser = proxyRefs(user);
    expect(user.age.value).toBe(18);
    expect(proxyUser.age).toBe(18);
    expect(proxyUser.name).toBe("Reiner");

	proxyUser.age = 20;
    expect(proxyUser.age).toBe(20);
    expect(user.age.value).toBe(20);

    proxyUser.age = ref(20);
    expect(proxyUser.age).toBe(20);
    expect(user.age.value).toBe(20);
   });
});
```