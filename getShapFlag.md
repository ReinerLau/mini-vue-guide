# 实现 shapFlags

```ts
import { ShapFlags } from '../shared/ShapFlags'
function getShapFlag(type){
	return typeof type === 'string' ? ShapFlags.ELEMENT : ShapFlags.STATEFUL_COMPOMENT
}
```
