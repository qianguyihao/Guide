

## 什么导致了 1px 问题？

如果使用 css 的 `1px` 来设置 border ，那么在Retine高清屏上， 可能会出现比较粗的情况。<br>

比如有些手机屏幕的 DPR = 2 ，即 `1px` 会用两个物理像素来显示，就比较粗了。

```css
.div1 {
  	padding: 10px 0;
    border-bottom: 1px solid #eee;
}
```

但我们也不能直接写 `0.5px` ，因为有些浏览器兼容性不好，渲染出来可能还是 `1px` 的效果。

## 解决办法：使用 `transform` 缩小

我们可以使用 css 伪类 + `transform` 来解决这一问题。即把默认的 `1px` 宽度设置为 0.5px。

代码实现：

```css
.box1 {
    padding: 10px 0;
    position: relative;
}
.box1::before {
    content: '';
    position: absolute;
    left: 0;
    bottom: 0;
    width: 100%;
    height: 1px;
    background: #d9d9d9;
    transform: scaleY(0.5);
    transform-origin: 0 0;
}
```

## 追问：如果有 `border-radius` 怎么办

可以使用 `box-shadow` 设置

- X 偏移量 `0`
- Y 偏移量 `0`
- 阴影模糊半径 `0`
- 阴影扩散半径 `0.5px`
- 阴影颜色

```css
.box2 {
    margin-top: 20px;
    padding: 10px;
    border-radius: 5px;
    box-shadow: 0 0 0 0.5px #d9d9d9;
}
```



## 参考链接

- [如何解决移动端 Retina 屏 1px 像素问题 ？ - 掘金](https://juejin.cn/post/6994196887402184734#heading-6)