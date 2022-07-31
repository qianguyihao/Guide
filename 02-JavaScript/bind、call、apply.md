## bind

### 介绍

- 返回一个新函数，但不执行
- 绑定this和部分参数
- 如果是箭头函数，则无法改变this，只能改变参数

### 手写 bind 函数

```js
Function.prototype.customBind = function (context, ...bindArgs) {
    // context 是 bind 传入的 this
    // bindArgs 是 bind 传入的各个参数

    const self = this // 当前的函数本身

    return function (...args) {
        // 拼接参数
        const newArgs = bindArgs.concat(args)
        return self.apply(context, newArgs)
    }
}
```