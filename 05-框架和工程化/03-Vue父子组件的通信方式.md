## Vue父子组件通信方式

### props 和 $emit



### 组件之间的通信：自定义事件

如果组件A和组件B是兄弟组件，或者这两个组件隔得比较远，则可以用如下方式进行通信：

组件A，注册自定义事件：

```js
event.$emit('myEvent', params);
```

组件B，监听事件：

```js
mounted() {
  // 监听自定义事件
  event.$on('myEvent', params);
}

beforeDestroy() {
  // 及时销毁，否则可能造成内存泄漏【重要】
  event.$off('myEvent', this.)
}
```

上方代码的 event 是Vue实例自带的。



### ref



### vuex