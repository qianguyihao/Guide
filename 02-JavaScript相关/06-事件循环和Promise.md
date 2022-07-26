

## Event Loop 事件循环 



### 任务队列



所有任务可以分成两种，一种是同步任务（synchronous），另一种是异步任务（asynchronous）。同步任务指的是，在主线程上排队执行的任务，只有前一个任务执行完毕，才能执行后一个任务。异步任务指的是，不进入主线程、而进入"任务队列"（task queue）的任务，只有"任务队列"通知主线程，某个异步任务可以执行了，该任务才会进入主线程执行。


总结：**只要主线程空了，就会去读取"任务队列"，这就是JavaScript的运行机制**。【重要】

### Event Loop 事件循环机制

主线程从"任务队列"中读取事件，这个过程是循环不断的，所以整个的这种运行机制又称为Event Loop（事件循环）。

JS是单线程的，异步任务要基于回调来实现。Event Loop 就是异步回调的实现原理。

![](https://img.smyhvae.com/20180310_1840.png)

Event Loop的过程：

（1）同步代码，一行一行放在 Call Stack 执行。

（2）遇到异步，会先“记录”下，等待时机（定时、网络请求等）

（3）时机到了，就移动到 Callback Queue。

（4）如果 Call Stack 为空（即同步代码执行完）Event Loop 开始工作。

（5）轮询查找 Callback Queue，如有则移动到Call Stack 执行。

（6）继续轮询查找。

在理解Event Loop时，要理解两句话：

- 理解哪些语句会放入异步任务队列

- 理解语句放入异步任务队列的**时机**


### 容易答错的题目

```javascript
    for (var i = 0; i < 3; i++) {
        setTimeout(function () {
            console.log(i);
        }, 1000);
    }
```

很多人以为上面的题目，答案是`0,1,2,3`。其实，正确的答案是：`3,3,3,3`。

分析：for 循环是同步任务，setTimeout是异步任务。for循环每次遍历的时候，遇到settimeout，就先暂留着，等同步任务全部执行完毕（此时，i已经等于3了），再执行异步任务。


我们把上面的题目再加一行代码。最终代码如下：

```javascript
    for (var i = 0; i < 3; i++) {
        setTimeout(function () {
            console.log(i);
        }, 1000);
    }
    console.log(i);
```

如果我们约定，用箭头表示其前后的两次输出之间有 1 秒的时间间隔，而逗号表示其前后的两次输出之间的时间间隔可以忽略，代码实际运行的结果该如何描述？可能会有两种答案：

- A. 60% 的人会描述为：`3 -> 3 -> 3 -> 3`，即每个 3 之间都有 1 秒的时间间隔；

- B. 40% 的人会描述为：`3 -> 3,3,3`，即第 1 个 3 直接输出，1 秒之后，连续输出 3 个 3。

循环执行过程中，几乎同时设置了 3 个定时器，这些定时器都会在 1 秒之后触发，而循环完的输出是立即执行的，显而易见，正确的描述是 B。

上面这个题目的参考链接：

- [80% 应聘者都不及格的 JS 面试题](https://juejin.im/post/58cf180b0ce4630057d6727c)

- [深入浅出Javascript事件循环机制(上)](https://zhuanlan.zhihu.com/p/26229293)



## Promise

### promise 基本用法

详见 Web前端图文教程。

### 手写 promise，加载一张图片



### Promise 有哪三种状态？如何变化？

三种状态：

- pending、resolved、rejected
- pending→rejected 或 pending→resolved
- 变化不可逆

如何变化：

- pending 状态，不会触发 then和catch
- resolved 状态，会触发后续的 then 回调函数
- rejected 状态，会触发后续的 catch 回调函数

### then 和 catch 如何改变 Promise 状态【重要】

- then里面，只要没报错，则返回 resolved 状态的Promise；如果有报错则返回 rejected状态的 Promise。
- catch里面，只要没报错，则返回 resolved 状态的Promise；如果有报错则返回 rejected状态的 Promise。

### 其他问题

- then 和 catch的链式调用
- 手写 promise
- 



## async await

### async await的引入

- 早期：异步回调 callback hell

- 进阶：Promise的then catch 链式调用，但也是基于回调函数

- 高阶：async／await 是同步语法。用同步语法写异步代码，彻底消灭回调函数的写法。

### async await 和 Promise的联系

- 执行async函数，返回的是Promise对象。不管  async 函数里面是什么内容。

- await 相当于Promise then

- try...catch 可捕获异常，代替 Promise 的 catch

async await 只是语法糖，异步的本质仍是回调函数。



## for of 常用于异步遍历

我们知道，for循环、forEach循环是同步遍历数组。而 for of是异步遍历数组。

```js
(async function () {
  for (let i of arr) {
    const res = await myPromise(i);
    console.log(res);
  }
})();
```



## 宏任务macroTask和微任务microTask

### 哪些是宏任务、微任务

- 宏任务：setTimeout、setInterval、Ajax、DOM事件
- 微任务：Promise、async await
- **微任务执行时机比宏任务要早**

### event loop 和  DOM渲染的关系

JS执行时，和DOM渲染共一个线程。

JS执行时，得留一些时机供DOM渲染。

### 为什么微任务比宏任务执行更早

直接原因：

- 宏任务：DOM渲染后触发
- 微任务：DOM渲染前触发。

根本原因：

- 微任务是ES6语法规定的。
- 宏任务是浏览器规定的。

事件循环机制的步骤：

（1）Call Stack 清空

（2）执行当前的微任务

（3）尝试DOM渲染

（4）执行当前的宏任务

（5）轮询 event loop。
