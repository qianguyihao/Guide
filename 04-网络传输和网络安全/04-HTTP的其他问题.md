
## http 1.0、1.1、2.0 的区别

http 1.0：

- 最基础的 http 协议。

- 支持基本的 get、post方法。

http 1.1：

- 增加新的 method `PUT` `DELETE` 等，可以设计 Restful API。
- 引入更多的缓存策略，如 `cache-control` 、`E-tag`。
- 断点续传，状态码 `206`。
- 长链接，默认开启 `Connection: keep-alive` ，多次 http 请求减少了 TCP 连接次数。

http2.0：

- 多路复用：一个 TCP 连接中可以包含多个 http 并行请求。此时，将不再需要做拼接资源（如CSS雪碧图、多 js 文件的合并为一个等）。
- header 压缩，以减少体积。比如 cookie 就是在 header里。
- 服务端推送。