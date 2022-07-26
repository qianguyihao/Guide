## 共同点

1. 都使用Virtural DOM
2. 都使用组件化思想，流程基本一致
3. 都是响应式，推崇单向数据流
4. 都有成熟的社区，都支持服务端渲染

## 区别

1、核心思想不同。

2、响应式原理不同。Vue依赖收集，自动优化；React基于状态机，手动优化。

3、diff算法不同。Vue Diff使用双向链表，边对比，边更新DOM。React主要使用diff队列保存需要更新哪些DOM，得到patch树，再统一操作批量更新DOM。



## Vue 和React越来越接近

- Vue3的Options API 对应 React class Component 
- Vue3的 Composition API 对应 React Hooks
- 不要再纠结哪个好，哪个坏



## 参考链接

- [个人理解Vue和React区别](https://lq782655835.github.io/blogs/vue/diff-vue-vs-react.html)

- [面试官：谈谈Vue和React的区别？](https://jishuin.proginn.com/p/763bfbd54ab9)