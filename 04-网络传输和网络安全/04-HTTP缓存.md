

## 关于http 缓存

### 概念

浏览器首次访问服务端时，资源文件（比如图片）会在**本地的硬盘**里存有副本；浏览器下次请求的时候，可能直接从本地读取，而不会重新请求服务器端资源。从而使得网络请求更快，用户体验更好。

### 哪些资源需要缓存

1、哪些资源需要缓存：

- 静态资源：js、css、img

静态资源上线后，不会再被修改。每个静态文件，在编译打包时，会加上**唯一的 hash值**放在文件名的后缀中，然后发布到线上环境。

2、哪些资源不需要缓存：（需要随时更新的数据）

- html文件。开发者可能随时发布新的页面。
- 业务数据。比如文章的评论数据，后端可能随时做增删改查。

### http 缓存分类

http 缓存策略分为：

- 强缓存

- 协商缓存

## 强缓存

**强缓存**：不用请求服务器，直接使用本地缓存。

强缓存是利用 response headers（http响应头）中的**`Expires`**或**`Cache-Control`**实现的。【重要】

浏览器第一次请求一个资源时，服务器在返回该资源的同时，会把上面这两个属性放在response headers中。比如：

![](https://img.smyhvae.com/20180310_2310.png)

**注意**：这两个response header属性可以只启用一个，也可以同时启用。当response header中，Expires和Cache-Control同时存在时，**Cache-Control的优先级高于Expires**。

下面讲一下二者的区别。

**1、`Expires`**：服务器返回的**绝对时间**。

是较老的强缓存管理 response header。浏览器再次请求这个资源时，先从缓存中寻找，找到这个资源后，拿出它的Expires跟当前的请求时间比较，如果请求时间在Expires的时间之前，就能命中缓存，否则就不行。

如果缓存没有命中，浏览器直接从服务器请求资源时，Expires Header在重新请求的时候会被更新。

**缺点：**

由于`Expires`是服务器返回的一个绝对时间，存在的问题是：服务器的事件和客户端的事件可能不一致。在服务器时间与客户端时间相差较大时，缓存管理容易出现问题，比如随意修改客户端时间，就能影响缓存命中的结果。所以，在http1.1中，提出了一个新的response header，就是Cache-Control。

**2、`Cache-Control`**：服务器返回的**相对时间**。

http1.1中新增的 response header。浏览器第一次请求资源之后，在接下来的相对时间之内，都可以利用本地缓存。超出这个时间之后，则不能命中缓存。重新请求时，`Cache-Control`会被更新。

比如 `Cache-control: max-age=31536000`（单位是秒）的意思是缓存一年。



## 协商缓存

**协商缓存**：浏览器发现本地有资源的副本，但是不太确定要不要使用，于是去问问服务器。

当浏览器对某个资源的请求没有命中强缓存（也就是说超出时间了），就会发一个请求到服务器，验证协商缓存是否命中。

协商缓存是利用的是两对Header：

- 第一对：`Last-Modified`、`If-Modified-Since`

- 第二对：`ETag`、`If-None-Match`

ETag（Entity Tag）：被请求变量的实体值”。

**1、`Last-Modified`、`If-Modified-Since`**。过程如下：

（1）浏览器第一次请求一个资源，服务器在返回这个资源的同时，会加上`Last-Modified`，这个header表示这个资源在服务器上的最后修改时间：

![](https://img.smyhvae.com/20180311_1715.png)

（2）浏览器再次请求这个资源时，会加上`If-Modified-Since`这个 request header，这个header的值就是上一次返回的`Last-Modified`的值：

![](https://img.smyhvae.com/20180311_1716.png)

（3）服务器收到第二次请求时，会比对浏览器传过来的`If-Modified-Since`和资源在服务器上的最后修改时间`Last-Modified`，判断资源是否有变化。如果没有变化则返回304 Not Modified，但不返回资源内容（此时，服务器不会返回 Last-Modified 这个 response header）；如果有变化，就正常返回资源内容（继续重复整个流程）。这是服务器返回304时的response header：

![](https://img.smyhvae.com/20180311_1720.png)

（4）浏览器如果收到304的响应，就会从缓存中加载资源。

**缺点：**

`Last-Modified`、`If-Modified-Since`一般来说都是非常可靠的，但面临的问题是：

- **服务器上的资源变化了，但是最后的修改时间却没有变化**。


- 如果服务器端在一秒内修改文件两次，但产生的`Last-Modified`却只有一个值。

这一对header就无法解决这种情况。于是，下面这一对header出场了。



**2、`ETag`、`If-None-Match`**。过程如下：

（1）浏览器第一次请求一个资源，服务器在返回这个资源的同时，会加上`ETag`这个 response header，这个header是服务器根据当前请求的资源生成的**唯一标识**。这个唯一标识是一个字符串，只要资源有变化这个串就不同，跟最后修改时间无关，所以也就很好地补充了`Last-Modified`的不足。如下：

![](https://img.smyhvae.com/20180311_1735.png)

（2）浏览器再次请求这个资源时，会加上`If-None-Match`这个 request header，这个header的值就是上一次返回的`ETag`的值：

![](https://img.smyhvae.com/20180311_1737.png)

3）服务器第二次请求时，会对比浏览器传过来的`If-None-Match`和服务器重新生成的一个新的`ETag`，判断资源是否有变化。如果没有变化则返回304 Not Modified，但不返回资源内容（此时，由于ETag重新生成过，response header中还会把这个ETag返回，即使这个ETag并无变化）。如果有变化，就正常返回资源内容（继续重复整个流程）。这是服务器返回304时的response header：

![](https://img.smyhvae.com/20180311_1740.png)

（4）浏览器如果收到304的响应，就会从缓存中加载资源。

提示：如果面试官问你：与浏览器缓存相关的http header有哪些？你能默写出来吗？这是一个亮点。

## 参考链接

- [浏览器缓存知识小结及应用](https://www.cnblogs.com/lyzg/p/5125934.html)
- [一文彻底搞懂http缓存，图文解说+实战应用 - 掘金](https://juejin.cn/post/7051552782486077471)
- [前端基础知识艾宾浩斯记忆（anki） | 前端基础知识艾宾浩斯记忆](https://80264867.xyz/)