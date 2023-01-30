# 实现 getCurrentInstance

作为中间层，方便 debug
```ts
let currentInstance
function setCurrentInstance(value){
	currentInstance = value
}
```