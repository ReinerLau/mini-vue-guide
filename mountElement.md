# 初始化 element

```ts
function mountElement(vnode, container) {
  const el = document.createElement(vnode.type);

  const { children } = vnode;
  if (typeof children === "string") {
    el.textContent = children;
  } else if (Array.isArray(children)) {
    mountChildern(vnode, el);
  }

  const { props } = vnode;
  for (const key in props) {
    const val = props[key];
    el.setAttribute(key, val);
  }

  container.append(el);
}
```

[[mountChildren#初始化 element]]