## 前言

目前比较流行的 Node.js 框架有Express、KOA 和 Egg.js，其次是另外一个正在兴起的与 TypeScript 相关的框架——Nest.js。

无论是哪个 Node.js 框架，都是基于中间件（可以理解为一个类或者函数模块）来实现的，而中间件的执行方式就需要依据洋葱模型来介绍。**Express 和 KOA 之间的区别也在于洋葱模型的执行方式上**。

## 洋葱模型

### koa2 介绍

1、随着 Node.js 的不断迭代，出现了以 await/async 为核心的语法糖，Express 原班人马为了实现一个高可用、高性能、更健壮，并且符合当前 Node.js 版本的框架，开发出了 KOA 框架。

2、koa2是非常**轻量、精简**的 Node.js框架。

如果我们不进行二次开发，基本什么东西都没有。koa2的设计思想非常超前和优秀，但是缺少辅助性的库。越是精简的框架，**定制化能力**就越强，开发者可以按照自己的喜好做二次开发和封装。

3、koa2通过**中间件**的形式组织代码，多个中间件以“**洋葱模型**”执行。【重要】



### 代码示例

koa官网 <https://koa.bootcss.com/> 或者  <http://koajs.cn/>有个示例：

```js
const Koa = require('koa');
const app = new Koa();

// logger
app.use(async (ctx, next) => {
  await next(); // 先执行下一步 x-response-time，执行完成后再继续执行当前的 logger
  const rt = ctx.response.get('X-Response-Time');
  console.log(`${ctx.method} ${ctx.url}：${rt}`);
});

// x-response-time
app.use(async (ctx, next) => {
  const start = Date.now();
  await next(); // // 先执行下一步 response，执行完成后再继续执行当前的 x-response-time
  const ms = Date.now() - start; // 统计 response 中间件的响应时间
  ctx.set('X-Response-Time', `${ms}ms`);
});

// response
app.use(async ctx => {
  ctx.body = 'Hello World';
});

app.listen(3000);
```

代码解释：

（1）注册中间件：上面有三个函数，通过`app.use()`注册之后，这几个函数就形成了中间件。

（2）当一个中间件A遇到 next() 时，则该中间件暂停，然后执行下一个中间件B；当B执行完成后，再回来执行A



### 图形解释

图1：

![image-20220731112947371](https://img.smyhvae.com/image-20220731112947371.png)

图2：

![20220731_1133](https://img.smyhvae.com/20220731_1133.png)

图2中，中间的竖线代表 next()。

## Express 和 KOA的差异

（1）Express 封装、内置了很多中间件，比如 connect 和 router ，而 KOA 则比较轻量，开发者可以根据自身需求定制框架；

（2）Express 是基于 callback 来处理中间件的，而 KOA 则是基于 await/async；

（3）在异步执行中间件时，Express 并非严格按照洋葱模型执行中间件，而 KOA 则是严格遵循的。