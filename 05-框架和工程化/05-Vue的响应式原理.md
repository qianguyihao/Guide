## 考点

- Vue 响应式原理
- Vue 虚拟 DOM 相关原理
- diff算法
- Vue 模板编译原理
- Vue 组件渲染过程

## MVVM：数据驱动视图



## Vue2响应式原理

### Object.defineProperty：监听 data 变化的核心API

data发生变化，立即触发视图更新。

Object.defineProperty的基本用法：（如何实现响应式，代码演示）


### 复杂对象，深度监听

递归。

### Object.defineProperty 的缺点

Object.defineProperty 也有一些缺点，Vue3的 Proxy改进了这一点。但是 Proxy也有兼容性问题，且无法 polyfill。

Object.defineProperty的缺点：

- 深度监听，需要递归到底，一次性计算量大。
- 无法监听新增属性／删除属性（可以通过 Vue.set、Vue.delete解决） 。
- 无法原生监听数组，需要特殊处理？

### 如何监听数组变化



## Vue3响应式：Proxy





## Vue3的Options API 对应 React class Component



## Vue3的 Composition API 对应 React Hooks
