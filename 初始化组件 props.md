保存 vnode 上的 props 到组件实例上

[[初始化组件 state]]时作为 setup 方法参数传入

props 是只可读的（浅层）

render 中读取 props 则是需要[[组件代理对象]]判断属性是否存在在状态对象上，再判断是否存在在 props