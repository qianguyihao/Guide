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



## Vue组件的生命周期（包括有父子组件时的情况）

### 单个组件

（1）创建阶段：beforeCreate、created。Vue实例初始化完成，页面尚未渲染完成。

（2）渲染阶段：beforeMount、mounted。页面渲染完成。大部分业务逻辑需要在 mounted里做。

（3）更新阶段：beforeUpdate、updated。data被修改时

（4）销毁阶段：beforeDestroy、destroyed。需要在 beforeDestroy里做的是：销毁自定义事件、清除定时任务、

### 父子组件的生命周期

（1）创建阶段：父组件先执行，子组件后执行。

父beforeCreate-> 父created -> 子beforeCreate-> 子created

（2）渲染阶段：子组件先执行，父组件后执行。因为子组件渲染完，父组件才能渲染完。

子mounted -> 父mounted

（3）更新阶段：父 beforeUpdate -> 子 beforeUpdate -> 子 updated -> 父updated







## 描述组件渲染和更新的过程



## 双向数据绑定 v-model 的实现原理



