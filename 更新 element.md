要在 render 中访问 ref 值而不需要使用 .value，可以在[[处理状态对象]]时使用[[代理响应式值]]

触发视图更新的关键在于将[[渲染组件]]的过程视作[[创建依赖|依赖]]被[[收集依赖|收集]]起来，在响应式依赖更新后[[触发依赖]]导致调用render 重新渲染进而实现视图更新

组件实例本身需要一个标记区分首次挂载还是更新

如果是更新的话还要在[[拆箱]]时传入旧 vnode 在[[处理元素]]中比对前后变化