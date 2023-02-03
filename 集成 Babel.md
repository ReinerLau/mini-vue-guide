babel 的作用是对新版本的 JavaScript 语法向后兼容，支持在不同环境下的运行

比如将[[集成 Jest]]中的例子改成使用 esm 规范，这时运行测试就会报 SyntaxError: Cannot use import statement outside a module 错误，因为 node 环境不支持 esm 规范，只支持 commanjs 规范
```js
// sum.js
function sum(a, b) {
  return a + b;
}

export default sum;
```

```js
// sum.spec.js
import sum from "../sum";

test("adds 1 + 2 to equal 3", () => {
  expect(sum(1, 2)).toBe(3);
});
```

安装
```shell
yarn add babel-jest @babel/core @babel/preset-env -D
```

配置，指定 node 版本为当前版本
```js
// babel.config.js
module.exports = {
  presets: [["@babel/preset-env", { targets: { node: "current" } }]],
};
```

# 相关资料

[Babel 是什么？](https://www.babeljs.cn/docs/index.html)
[Getting Started](https://jestjs.io/docs/getting-started#using-babel)