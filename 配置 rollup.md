安装
```shell
yarn add rollup -D
```

添加 rollup 配置文件，支持 esm 规范
```js
// rollup.config.mjs
export default {}
```

指定库的入口文件
```diff
export default {
+	input: "./src/index.ts"
}
```

指定库最终打包的几种模块规范
```diff
export default {
+	output: [
+		 {
+			format: "cjs",
+			file: "lib/mini-vue.cjs.js"
+		 },
+		{
+			format: "es",
+			file: "lib/mini-vue.esm.js"
+		}
+	]
}
```

支持 typescript
```shell
yarn add @rollup/plugin-typescript -D
```

```diff
+ import typescript from '@rollup/plugin-typescript'
export default {
+	plugins: [typescript()]
}
```

配置打包脚本
```json
{
	"scripts": {
		"build": "rollup -c rollup.config.mjs"
	}
}
```
