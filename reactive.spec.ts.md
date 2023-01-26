```ts
import { reactive } from "../reactive";

describe("reactive", () => {
  it("happy path", () => {
    const orignal = { foo: 1 };
    const observed = reactive(orignal);
    expect(observed).not.toBe(orignal);
    expect(observed.foo).toBe(1);
  });
});
```

[[reactive#创建代理对象|reactive]] 返回响应式对象

[[reactive#get|读取]]响应式对象属性