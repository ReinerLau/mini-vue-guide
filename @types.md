某些第三方库本身不是用 typescript 写的，也就没有类型声明文件，或者第三方库是用 typescript 写的，但没有导出类型声明文件，这时就需要我们自己写 .d.ts 类型声明文件

当然正常情况下，我们不需要为第三方库写声明，@types 类型的包已经帮我们定义好了第三方库的 .d,ts 类型声明文件，由 [DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped) 组织维护，涵盖了市面上所有流行的第三方库

默认情况下，typescript 的配置文件 tsconfig.json 有一个配置项 typeRoots 指向 node_modules/@types，所以 ts 会自动到该目录查找对应第三方库的类型声明文件，当然我们也可以手动指定多个目录去查找自定义的类型声明文件
```js
{
  "compilerOptions": {
	"typeRoots": ["node_modules/@types","./typings"]
  }
}
```

另外还有一个 types 配置，指定只引入哪些模块的类型声明
```js
{
  "compilerOptions": {
    "types" : ["node", "lodash", "express"]
  }
}
```

# 相关资料

[还不知道 TypeScript 怎么去查找类型定义的看这里 - 掘金](https://juejin.cn/post/7068230062323007519)
[TypeScript 入门教程](https://ts.xcatliu.com/basics/declaration-files.html)
[types 和 @types 是什么？- 知乎](https://zhuanlan.zhihu.com/p/194196536) 
[深入理解 TypeScript](https://jkchao.github.io/typescript-book-chinese/typings/types.html)