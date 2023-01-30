`src/runtime-core/component.ts`

创建组件实例
```ts
export function createComponentInstance(vnode) {
  const component = {
    vnode,
    type: vnode.type,
  };

  return component;
}
```

# 实现组件接收 props

```diff
export function createComponentInstance(vnode){
	const component = {
		vnode,
		type: vnode.type,
+		props: {} 
	}
	return component
}
```

# 实现组件 emit

```diff
+ import { emit } from './componentEmit'
export function createComponentInstance(vnode){
	const component = {
		vnode,
		type: vnode.type,
		props: {},
+		emit
	}
	return component
}
```

触发事件
```diff
import { emit } from './componentEmit'
export function createComponentInstance(vnode){
	const component = {
		vnode,
		type: vnode.type,
		props: {},
+		emit: emit.bind(null, componnet) 
	}
	return component
}
```