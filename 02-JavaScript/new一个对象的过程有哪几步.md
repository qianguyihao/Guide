
## new 一个对象的过程有哪几步

（1）创建一个空对象（实例对象），继承构造函数的原型

（2）将 this 指向这个新的对象。

（3）执行构造函数里面的代码，给这个新对象添加属性和方法。

（4）返回这个新对象（所以构造函数里面不需要 return）。


## 手写 new，了解深层原理

class 是 function 的语法糖。

普通函数写法：

```js
function Foo(name) {
    this.name = name
    this.city = '深圳'
}
Foo.prototype.getName = function () { // 注意，这里不可以用箭头函数
    return this.name
}
const f = new Foo('千古壹号')
```

class写法：

```js
class Foo {
    constructor(name) {
        this.name = name
        this.city = '深圳'
    }
    getName() {
        return this.name
    }
}
const f = new Foo('千古壹号')
```

## 追问：Object.create() 和 {} 的区别

`Object.create()`：创建一个空对象，可以指定原型（原型指向传入的参数）。

`{}`：创建空对象，原型指向 Object.prototype。相当于 `Object.create(Object.prototype)` 。