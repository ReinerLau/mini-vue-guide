[[实现 effect]]
[[实现收集依赖]]
[[实现触发依赖]]
```ts
import { reactive } from "../reactive";
import { effect } from "../effect";

describe("effect", () => {
	it("happy path", () => {
		const user = reactive({
			age: 10,
		});
		let nextAge;
		effect(() => {
		  nextAge = user.age + 1;
		});
		expect(nextAge).toBe(11);
		user.age++;
		expect(nextAge).toBe(12);
	});
 })
```