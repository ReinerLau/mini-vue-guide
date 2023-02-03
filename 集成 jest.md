安装
```shell
yarn add jest -D
```

配置脚本
```json
// package.json
{
	"scripts" {
	   test": "jest"
	}
}
```

测试代码
`sum.js`
```js
// sum.js
function sum(a, b) {
  return a + b;
}
module.exports = sum;
```
`sum.spec.js`
```js
// sum.spec.js
const sum = require("./sum");

test("adds 1 + 2 to equal 3", () => {
  expect(sum(1, 2)).toBe(3);
});
```

运行测试
```shell
yarn test
```

# 相关资料

[Getting Started](https://jestjs.io/docs/getting-started)