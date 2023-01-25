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

[[reactive.ts]]