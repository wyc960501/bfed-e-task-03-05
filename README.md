## Vue 3.0 性能提升主要是通过哪几方面体现的

**响应式系统升级**

- Vue.js 2.x 中响应式系统的核心 defineProperty
- Vue.js 3.0 中使用 Proxy 对象重写响应式系统
  - Proxy 对象实现属性监听，初始化的时候不需要遍历所有的属性，再把属性通过 defineProperty 转换成 get 和 set
  - 如果有多层属性嵌套，只有在访问属性过程中才会递归处理下一级属性
  - 可以监听动态新增的属性
  - 可以监听删除的属性
  - 可以监听数组的索引和 length 属性

**编译优化**

- Vue.js 2.x 中通过标记静态根节点，优化 diff 的过程

  - 静态节点还需要 diff ,这个过程没有被优化

- Vue.js 3.0 中标记和提升所有的静态根节点，diff 的时候只需要对比动态节点内容

  - Fragments (升级 vetur 插件)
  - 静态提升
  - Patch flag
  - 缓存事件处理函数

**优化打包体积**

- Vue.js 3.0 中移除了一些不常用的 API

  - 例如：inline-template、filter 等(最终让代码体积减小)

- Tree-shaking（支持更好）

## Vue 3.0 所采用的 Composition Api 与 Vue 2.x 使用的 Options Api 有什么区别

- Options API

  - 包含一个描述组件选项（data、methods、props 等）的对象
  - Options API 开发复杂组件，同一个功能逻辑的代码被拆分到不同选项

- Composition API

  - Vue.js 3.0 新增的一组 API
  - 一组基于函数的 API
  - 可以更灵活的组织组件的逻辑

## Proxy 相对于 Object.defineProperty 有哪些优点

- Proxy 对象实现属性监听，初始化的时候不需要遍历所有的属性，再把属性通过 defineProperty 转换成 get 和 set
- 如果有多层属性嵌套，只有在访问属性过程中才会递归处理下一级属性
- 默认监听动态添加的属性
- 默认监听属性的删除操作
- 默认监听数组索引和 length 属性

## Vue 3.0 在编译方面有哪些优化

- Vue.js 3.0 中标记和提升所有的静态根节点，diff 的时候只需要对比动态节点内容

  - Fragments (升级 vetur 插件)
  - 静态提升
  - Patch flag
  - 缓存事件处理函数

## Vue.js 3.0 响应式系统的实现原理

- 通过 effect 声明依赖响应式数据的函数 cb，并执行 cb 函数，执行过程中，会触发响应式数据 getter
- 在响应式数据 getter 中进行 track 依赖收集，建立数据和 cb 的映射关系存储于 targetMap
- 当变更响应式数据时，触发 trigger ，根据 targetMap 找到关联的 cb 执行
- 映射关系 targetMap
