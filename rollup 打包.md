rollup 一般用于库的打包， webpack 一般用于应用的打包

安装
```shell
yarn add rollup -D
```

配置打包入口
`rollup.config.mjs`
```js
export default {
  input: "./src/index.ts",
};
```

配置多种规范的打包出口
`rollup.config.mjs`
```diff
export default {
  input: "./src/index.ts",
+  output: [
+    {
+      format: "cjs",
+      file: "lib/mini-vue.cjs.js",
+    },
+    {
+      format: "es",
+      file: "lib/mini-vue.esm.js",
+    },
+  ],
};
```

支持 typescript
```shell
yarn add @rollup/plugin-typescript -D
```

`rollup.config.mjs`
```diff
+ import typescript from "@rollup/plugin-typescript";

export default {
  input: "./src/index.ts",
  output: [
    {
      format: "cjs",
      file: "lib/mini-vue.cjs.js",
    },
    {
      format: "es",
      file: "lib/mini-vue.esm.js",
    },
  ],
+  plugins: [typescript()],
};
```

打包脚本
`package.json`
```json
{
	"scripts": {
	    "build": "rollup -c rollup.config.js"
	},
}
```