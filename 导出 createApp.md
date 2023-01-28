页面引入 createApp
```js
// main.js
import { App } from './App.js'
import { createApp } from '../../lib/mini-vue.esm.js'

const rootContainer = document.querySelector('#app')
createApp(App).mount(rootContainer)
```
[[createApp]]

runtime-core 模块导出 createApp
```ts
// src/runtime-core/index.ts
export { createApp } from './createApp'
```

入口文件导出整个 runtime-core 模块
```ts
// src/index.ts
export * from './runtime-core/index'
```