## Vue和React的区别

### 共同点

1. 都使用Virtural DOM
2. 都使用组件化思想，流程基本一致
3. 都是响应式，推崇单向数据流
4. 都有成熟的社区，都支持服务端渲染

### 区别

1、核心思想不同。

2、响应式原理不同。Vue依赖收集，自动优化；React基于状态机，手动优化。

3、diff算法不同。Vue Diff使用双向链表，边对比，边更新DOM。React主要使用diff队列保存需要更新哪些DOM，得到patch树，再统一操作批量更新DOM。



### Vue 和React越来越接近

- Vue3的Options API 对应 React class Component
- Vue3的 Composition API 对应 React Hooks
- 不要再纠结哪个好，哪个坏



### 参考链接

- [个人理解Vue和React区别](https://lq782655835.github.io/blogs/vue/diff-vue-vs-react.html)

- [面试官：谈谈Vue和React的区别？](https://jishuin.proginn.com/p/763bfbd54ab9)

## Vue2、Vue3、React的diff 算法有什么区别

### diff算法初探

一般来说，如果要严格 diff 两棵树，时间复杂度为O（n^3）。不可用。

Vue和react算法都进行了diff算法的优化，时间复杂度O（n）。

### Vue和 react的diff 算法-共同点

- 只比较同一层级，不跨级比较
- 标签不同则删除重建，不再进行深度比较。
- 标签和key如果都都相同，则认为是相同节点，不再深度比较。

### Vue和 react的diff 算法-区别

- Vue2：双端diff。
- Vue3：最长递增子序列。
- React：仅右移。
