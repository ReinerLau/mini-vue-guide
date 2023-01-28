# 初始化 component

```ts
function handleSetupResult(instance, setupResult) {
  if (typeof setupResult === "object") {
    instance.setupState = setupResult;
  }

  finishComponentSetup(instance);
}
```

[[finishComponentSetup#初始化 component]]