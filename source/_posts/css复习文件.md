---
title: CSS复习
date: 2021-05-21 14:25:26
tags: 
 - 前端
 - CSS
categories:
 - 前端
 - CSS
description: 复习知识-CSS
---

# BFC
## 什么是BFC
> BFC(块格式化上下文)：是Web可视化渲染CSS的一部分，是布局过程中生成块级盒子的区域，也是浮动元素和其他元素交互的限定区域。
> 简单来说具备BFC特性的元素就相当于被一个容器包裹，容器内的元素在布局上不会影响外部元素

## BFC常见应用
> 1. 解决普通文档流块元素的外边距折叠问题
![外边距折叠](https://user-gold-cdn.xitu.io/2019/2/21/1690bb63f3eebe99?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

```js
<style>
    .demo {
        overflow: hidden;
    }
    .demo div {
        width: 40px;
        height: 40px
    }
    .demo1 {
        margin 10px 0;
        background: pink;
    }
    .demo2 {
        margin: 20px 0;
        background: blue;
    }
</style>

<div class="demo">
    <div class="demo1"></div>
</div>
<div class="demo">
    <div class="demo2"></div>
</div>
```
使用BFC解决
```js
<style>
    * {
        margin: 0;
        padding: 0;
    }
    .demo {
        overflow: hidden;
    }
    .demo div {
        width: 40px;
        height: 40px;
    }
    .demo1 {
        margin: 10px 0;
        background: pink;
    }
    .demo2 {
        margin: 20px 0;
        background: blue;
    }
</style>

<div class="demo">
    <div class="demo1"></div>
</div>
<div class="demo">
    <div class="demo2"></div>
</div>
```

> 2. BFC清浮动
![父级盒子高度](https://user-gold-cdn.xitu.io/2019/2/21/1690bb99839f6de1?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
```js
<style>
    * {
        margin: 0;
        padding: 0;
    }
    .demo {
        border: 1px solid pink;
    }
    .demo p {
        float: left;
        width: 100px;
        height: 100px;
        background: blue;
    }
</style>
<div class="demo">
    <p></p>
</div>
```
解决方法
```js
.demo {
    border: 1px solid pink;
    overflow: hidden;
}
```

> 3. 阻止普通文档流被浮动元素覆盖
![元素被覆盖](https://user-gold-cdn.xitu.io/2019/2/21/1690bbfccb00357d?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
```js
<style>
    * {
        margin: 0;
        padding: 0;
    }
    .demo1 {
        width: 100px;
        height: 100px;
        float: left;
        background: pink
    }
    .demo2 {
        width: 200px;
        height: 200px;
        background: blue;
    }
</style>

<div class="demo">
    <div class="demo1">我是一个左侧浮动元素</div>
    <div class="demo2">我是一个没有设置浮动, 也没有触发BFC的元素</div>
</div>
``` 
解决方法：触发demo2的BFC
.demo2 {
    width: 200px;
    height: 200px;
    background: blue;
    overflow: hidden;
}

> 自适应两栏布局
```js
<style>
* {
    margin: 0;
    padding: 0;
}
.container {
}
.float {
    width: 200px;
    height: 100px;
    float: left;
    background: red;
    opacity: 0.3;
}

.main {
    background: green;
    height: 100px;
    overflow: hidden;
}
</style>

<div class="container">
    <div class="float">
        浮动元素
    </div>
    <div class="main">
        自适应
    </div>
</div>
```

## 如何触发BFC
1. 根元素或包含根元素的元素
2. 浮动元素（元素的 float 不是 none）
3. 绝对定位元素（元素的 position 为 absolute 或 fixed）
4. 行内块元素（元素的 display 为 inline-block）
5. 表格单元格（元素的 display为 table-cell，HTML表格单元格默认为该值）
6. 表格标题（元素的 display 为 table-caption，HTML表格标题默认为该值）
7. 匿名表格单元格元素（元素的 display为 table、table-row、 table-row-group、table-header-group、table-footer-group（分别是HTML table、row、tbody、thead、tfoot的默认属性）或 inline-table）
8. overflow 值不为 visible 的块元素
9. display 值为 flow-root 的元素
10. contain 值为 layout、content或 strict 的元素
11. 弹性元素（display为 flex 或 inline-flex元素的直接子元素）
12. 网格元素（display为 grid 或 inline-grid 元素的直接子元素）
13. 多列容器（元素的 column-count 或 column-width 不为 auto，包括 column-count 为 1）
14. column-span 为 all 的元素始终会创建一个新的BFC，即使该元素没有包裹在一个多列容器中（标准变更，Chrome bug）。

----------------

# position
## positon属性
### static
> static是position的默认属性值。如果省略position属性，浏览器就认为该元素是static属性。
> 这时浏览器会按照源码的顺序，决定每个元素的位置，这是'正常的页面流'每个块级元素占据自己的区块，互相之间不重叠，这个位置就是元素的默认位置
> **`要注意`** ：static定位所导致的元素位置，是浏览器决定的，所以这时候`top`,`right`,`bottom`,`left`，这四个属性无效
### absolute，relative,fixed

--------

# 重绘和回流
## 浏览器渲染机制
> - 浏览器采用流式布局
> - 浏览器会把HTML解析成DOM，CSS解析成CSSOM，DOM和CSSOM合并产生了渲染树
> - 有了Render Tree，我们就知道了所有节点的样式，然后计算他们的大小和位置，最后把节点渲染到页面上。

## 重绘
> 由于节点的几何属性发生改变或者由于样式发生改变而不会影响布局的，我们称之为重绘。例如：`outline`,`visibility`,`color`,`background-color`,等，重绘的代价很高，因为浏览器必须要验证其他节点的可见性

## 回流
> 如果几何属性或者布局发生改变就成为回流。回流是影响浏览器性能的关键，因为涉及到不分页面或者是整体页面的布局更新。一个元素的回流可能导致其所有子元素以及DOM中的其他节点，祖先节点元素的随后的回流

> 回流一定会重绘，重绘不一定回流

## 如何优化
> 现代浏览器都是通过队列机制来批量更新布局，浏览器会把修改操作放到队列中，至少一个浏览器刷新(16.6ms)才会清空队列,但是当回去布局信息时，队列可能影响这些属性或方法返回值的操作，即使没有，浏览器也会清空队列，触发回流和重绘来确保返回正确的值
主要包括以下属性或方法：
`offsetTop`、`offsetLeft`、`offsetWidth`、`offsetHeight`、`scrollTop`、`scrollLeft`、`scrollWidth`、`scrollHeight`、`clientTop`、`clientLeft`、`clientWidth`、`clientHeight`、`width`、`height`、`getComputedStyle()`、`getBoundingClientRect()`
所以，我们应该避免频繁的使用上述的属性，他们都会强制渲染刷新队列。

## 减少回流和重绘
> - CSS 
   + 使用`transform`代替`top`
   + 使用visibility代替display:none (前者会引发重绘，后置引起回流)
   + 尽可能在DOM树的最末端改变class，回流不可避免，但是可以减少其影响。尽量在dom树的末端改变class，可以限值回流的范围，使其影响尽可能少的节点。
   + 避免使用多层内联样式