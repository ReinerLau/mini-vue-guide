# 实现组件接收 props

```ts
export function initProps(instance, props){
	instance.props = props || {}	
}
```