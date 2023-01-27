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

[[实现 effect 返回 runner]]
```ts
import { effect } from "../effect";

describe("effect", () => {
  it("should return runner when call effect", () => {
    let foo = 10;
    const runner = effect(() => {
      foo++;
      return "foo";
    });

    expect(foo).toBe(11);
    const r = runner();
    expect(foo).toBe(12);
    expect(r).toBe("foo");
  });
});
```

[[实现 effect 的 scheduler]]
```ts
import { reactive } from "../reactive";
import { effect } from "../effect";

it("scheduler", () => {
	let dummy;
	let run;
	const scheduler = jest.fn(() => {
	  run = runner;
	});
	const obj = reactive({ foo: 1 });
	const runner = effect(
	  () => {
		dummy = obj.foo;
	  },
	  {
		scheduler,
	  }
	);
	
	expect(scheduler).not.toHaveBeenCalled();
	obj.foo++;
	expect(scheduler).toHaveBeenCalledTimes(1);
	expect(dummy).toBe(1);
	run();
	expect(dummy).toBe(2);
});
```

[[实现 effect 的 stop]]
[[重构 effect 的 stop ]]
[[优化 effect 的  stop]]
```ts
import { reactive } from "../reactive";
import { effect, stop } from "../effect";

it("stop", () => {
    let dummy;
    const obj = reactive({ prop: 1 });
    const runner = effect(() => {
      dummy = obj.prop;
    });
    obj.prop = 2;
    expect(dummy).toBe(2);
    stop(runner);
    obj.prop++;
    expect(dummy).toBe(2);
    runner();
    expect(dummy).toBe(3);
  });
```

[[实现 effect 的 onStop]]
[[重构 effect 的 onStop]]
```ts
import { reactive } from "../reactive";
import { effect, stop } from "../effect";

  it("onStop", () => {
    let dummy;
    const onStop = jest.fn(() => {});
    const obj = reactive({ foo: 1 });
    const runner = effect(
      () => {
        dummy = obj.foo;
      },
      {
        onStop,
      }
    );
    stop(runner);
    expect(onStop).toHaveBeenCalledTimes(1);
  });
```