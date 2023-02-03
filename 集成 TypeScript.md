安装（最新版有bug）
```shell
yarn add typescript@4.8.4 -D
```

使用
```shell
npx tsc src/index.ts
```

node 直接运行 ts 文件，安装 ts-node
```shell
yarn add ts-node -D
```

```shell
npx ts-node src/index.ts
```

jest 使用 babel 将 typescript 语法转换成 jest 认识的语法，现在运行 ts 的测试不会报错
```js
// babel.config.js
module.exports = {
  presets: [
    ["@babel/preset-env", { targets: { node: "current" } }],
    "@babel/preset-typescript",
  ],
};
```

此时 ts 文件会因为找不到 jest 的类型声明而报错，安装 @types/jest，关于 @types，看[[@types|这里]]
```shell
yarn add @types/jest -D
```

不关注类型，初始化 tsconfig.json 配置文件，关闭 any 检查
```shell
npx tsc --init
```

`tsconfig.json`
```json
// tsconfig.json
{
	"noImplicitAny": false
}
```

# 相关资料

[5分钟上手TypeScript](https://www.tslang.cn/docs/handbook/typescript-in-5-minutes.html)
[Getting Started](https://jestjs.io/docs/getting-started#using-typescript)