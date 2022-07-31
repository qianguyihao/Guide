## DOM操作

### property 和 attribute

- property：修改对象属性，不会体现到 html结构中。
- attribute：修改 html属性，会改变 html 结构。

两者都有可能引起 DOM 重绘。

### 如何优化 DOM操作性能

- 避免频繁操作 DOM。可以合并多个DOM操作，将频繁操作改为一次性操作。
- 对DOM查询做缓存。比如，把DOM的长度存到变量里，就不用每次都查。



## BOM操作

### 常见 API

- navigator。navigator.userAgent 获取浏览器信息。
- screen
- location
- History

