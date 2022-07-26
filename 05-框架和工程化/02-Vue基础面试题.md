## Vue基础面试题



### v-html

有 xss风险，会覆盖子组件。



### computed

computed有缓存。如果data不变则会重新计算。

### watch

- watch默认不会深度监听
- watch监听引用类型，拿不到 oldVal

### v-if 和 v-show 的区别

v-show：

- 值为 false时，DOM节点一直存在，属性是 display:none
- 如果频繁切换这个DOM节点的展示，建议用  v-show。避免DOM频繁地创建、销毁。

v-if：

- 值为false时，DOM节点不存在。
- 如果这个DOM节点不是经常展示，则建议使用 v-if。



### 为何 v-for 中要用 key





### v-for 和 v-if 不能一起使用

假设v-for 和 v-if一起使用：

- 由于v-for比 v-if先执行，这会导致 v-if重复执行很多遍。这种写法是不建议的。











## 描述 Vue组件生命周期（包括有父子组件时的情况）







## 父子组件通信方式





## 描述组件渲染和更新的过程



## 双向数据绑定 v-model 的实现原理



