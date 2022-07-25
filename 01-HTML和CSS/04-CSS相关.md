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
