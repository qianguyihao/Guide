## 盒模型相关

### 计算盒模型宽度

标准盒模型：

- offsetWidth = 内容宽度 + padding + border


### margin纵向重叠问题



### margin负值问题

## BFC的理解和应用

### 什么是 BFC

BFC：block format context，块级格式化上下文。是一块独立渲染区域，内部元素的渲染不会影响边界以外的元素。

### 形成 BFC 的条件

以下任何一个条件，都可以形成 BFC：

- float 不是 none（设置 float 属性即可）

- position 是 absolute 或 fixed

- overflow 不是 visible（比如 overflow:hidden）

- display 是 flex、inline-block等

### BFC的应用

- 清除浮动

## float布局及 clearfix


### 如何实现圣杯布局、双飞翼布局



### 手写 clearfix

```css
/* 手写 clearfix */
.clearfix:after {
    content: '';
    display: table;
    clear: both;
}

.clearfix {
    *zoom: 1; /* 兼容 IE 低版本 */
}

```

## flex布局

### 常见语法

- flex-direction

- justify-content

- align-items

- flex-wrap

- align-self

## CSS定位

### relative 和 absolute

- relative：依据自身定位

- absolute：依据最近一层的定位元素定位

### 如何让一个元素水平垂直居中

详见我的另外一篇文章：《[如何让一个元素水平垂直居中？](https://github.com/qianguyihao/Web/blob/master/03-CSS%E8%BF%9B%E9%98%B6/04-%E5%A6%82%E4%BD%95%E8%AE%A9%E4%B8%80%E4%B8%AA%E5%85%83%E7%B4%A0%E6%B0%B4%E5%B9%B3%E5%9E%82%E7%9B%B4%E5%B1%85%E4%B8%AD%EF%BC%9F.md)》

## CSS 其他样式

### line-height如何继承

- 如果写具体数值，则继承该值。
- 如果写百分比，则继承该比例（考点）。



## CSS响应式

### rem是什么

- px：绝对长度单位，常用。

- em：相对长度单位，相对于父元素，不常用
- rem：相对长度单位，相对于根元素，常用于响应式布局。r的意思是root。

常用写法举例：

```css
html: {
	font-size: 20px;
}

.my_div1 {
	font-size: 1rem;
}

.my_div2 {
	font-size: 2rem;
}
```





