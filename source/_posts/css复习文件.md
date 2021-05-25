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
> 简单来说具备BFC特性的元素就相当于被一个容器包裹，容器内的元素在布局上不会影响外部元素。

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

# CSS权重计算
> - 第一级：内联样式 如`style=""`，权重为1000
> - 第二级：id选择器 如`#content`，权重为100
> - 第三级：类选择器,伪类，属性选择器 如`.content`，权重为10
> - 第四级：标签选择器，伪元素选择器 如`.div p`，权重为1
>  + **`注意：`** 通用选择器(`*`)、子选择器(`>`)、相邻同胞选择器(`+`)，并不在这个等级中，所以他们的权重为0

----------------

# CSS像素单位
- **px**像素(Pixel)：相对长度单位。像素px是相对于显示器分辨率的
- **em**：相对长度单位。相对于当前父元素的字体尺寸。如果未设置，则相对于浏览器默认字体尺寸
- **rem**：CSS3新增的相对单位。使用rem为元素设定字体大小时，仍是相对大小，但相对的只是HTML根元素
- **view width**：是指可视窗口的宽度。假如宽度是1200px的话。那10vw就是120px
- **view height**：是指可视窗口的高度。假如高度是1200px的话。那10vh就是120px

-----------

# 定位
## positon属性
### static
> `static`是`position`的默认属性值。如果省略`position`属性，浏览器就认为该元素是`static`属性。
> 这时浏览器会按照源码的顺序，决定每个元素的位置，这是'正常的页面流'每个块级元素占据自己的区块，互相之间不重叠，这个位置就是元素的默认位置。
> **`要注意`** ：static定位所导致的元素位置，是浏览器决定的，所以这时候`top`,`right`,`bottom`,`left`，这四个属性无效。

### relative
> 相对定位方式相对与父元素进行定位，准确的说是相对于父元素所剩余未被占用的空间进行定位。且会占用该元素在文档中初始的页面空间，即在使用`top`等属性进行移动后依旧不会改变其所占空间的位置，可以使用`z-index`在z轴方向进行移动

### absolute
> 绝对定位方式，脱离文档流，不会占用页面空间。以最近的不是`static`定位的父级元素进行参考来定位，如果所有父级都是`static`定位，那就以当前窗口作为参考来进行定位。可以使用`top`、`bottom`、`left`、`right`进行位置移动，亦可使用`z-index`在z轴上面进行移动。当元素为此定位时，如果该元素为内联元素，则会变为块级元素，即可以直接设置其宽和高的值；如果该元素为块级元素，则其宽度会由初始的100%变为`auto`。

### fixed
> 绝对定位方式，直接以浏览器窗口作为参考进行定位。其它特性同absolute定位。当父元素使用了`transform`的时候，会以父元素定位。

--------

# 重绘和回流
## 浏览器渲染机制
> - 浏览器采用流式布局。
> - 浏览器会把HTML解析成DOM，CSS解析成CSSOM，DOM和CSSOM合并产生了渲染树。
> - 有了Render Tree，我们就知道了所有节点的样式，然后计算他们的大小和位置，最后把节点渲染到页面上。

## 重绘
> 由于节点的几何属性发生改变或者由于样式发生改变而不会影响布局的，我们称之为重绘。例如：`outline`,`visibility`,`color`,`background-color`,等，重绘的代价很高，因为浏览器必须要验证其他节点的可见性。

## 回流
> 如果几何属性或者布局发生改变就成为回流。回流是影响浏览器性能的关键，因为涉及到不分页面或者是整体页面的布局更新。一个元素的回流可能导致其所有子元素以及DOM中的其他节点，祖先节点元素的随后的回流。

> 回流一定会重绘，重绘不一定回流。

## 如何优化
> 现代浏览器都是通过队列机制来批量更新布局，浏览器会把修改操作放到队列中，至少一个浏览器刷新(16.6ms)才会清空队列,但是当回去布局信息时，队列可能影响这些属性或方法返回值的操作，即使没有，浏览器也会清空队列，触发回流和重绘来确保返回正确的值。
主要包括以下属性或方法：
`offsetTop`、`offsetLeft`、`offsetWidth`、`offsetHeight`、`scrollTop`、`scrollLeft`、`scrollWidth`、`scrollHeight`、`clientTop`、`clientLeft`、`clientWidth`、`clientHeight`、`width`、`height`、`getComputedStyle()`、`getBoundingClientRect()`
所以，我们应该避免频繁的使用上述的属性，他们都会强制渲染刷新队列。

## 减少回流和重绘
> - CSS 
>   + 使用`transform`代替`top`。
>   + 使用`visibility`代替`display:none` (前者会引发重绘，后置引起回流)。
>   + 尽可能在DOM树的最末端改变`class`，回流不可避免，但是可以减少其影响。尽量在dom树的末端改变`class`，可以限值回流的范围，使其影响尽可能少的节点。
>   + 避免使用多层内联样式，CSS从右往左匹配查找，避免节点层级过多。

```js
<div>
  <a> <span></span> </a>
</div>
<style>
  span {
    color: red;
  }
  div > a > span {
    color: red;
  }
</style>
```
>   + 将动画效果应用到`position`属性为`absolute`或`fixed`的元素上，避免影响其他元素布局，这样只是重绘，不是回流。
>   + 避免使用CSS表达式，可能会引起回流。
>   + 将频繁重绘或回流的节点设置为图层，图层能够组织该节点的渲染行为影响到其他节点，例如：`will-change`、`video`、`iframe`等标签，浏览器会自动奖该节点变为图层。
>   + CSS3硬件加速(GPU加速)：可以让`transform`、`opacity`、`filters`这些动画不会引起回流重绘 。但是对于动画的其它属性，比如`background-color`这些，还是会引起回流重绘的，不过它还是可以提升这些动画的性能。
> - JS
>   + 避免频繁操作样式：最好一次性重写`style`属性，或者将样式列表定义为`class`，并一次性更改`class`属性
>   + 避免频繁操作DOM：创建一个文档碎片(documentFragment)，在它上面应用所有DOM操作，最后再把它添加到文档中。
>   + 避免频繁读取会引发回流/重绘的属性，如果需要多次使用，用一个变量存起来。
>   + 对具有复杂动画的元素使用绝对定位：使他脱离文档流，否则会引起父级元素及后续元素频繁回流

## CSS3硬件加速(GPU加速)
> CSS3硬件加速，又叫GPU加速，是利用GPU渲染，减少CPU操作的一种优化方案。这是由于GPU中，`transform`等CSS属性不会触发repaint，能够大大提高网页性能。
> 详细介绍 [CSS3硬件加速介绍](https://lz5z.com/Web%E6%80%A7%E8%83%BD%E4%BC%98%E5%8C%96-CSS3%E7%A1%AC%E4%BB%B6%E5%8A%A0%E9%80%9F/)

-----------

# Flex
> [阮一峰Flex布局教程](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)

## Flex布局是什么
> Flex是`Flexible Box`的缩写，意思是弹性布局。为盒状模型提供最大灵活度。任何一个元素都可以指定为flex布局。

```js
.box {
    display: flex;
    }
```

> 行内元素也可以使用flex布局

```js
.box{
  display: inline-flex;
}
```
> 注意：设置为flex布局后，子元素的float、clear、和vertical-align属性都将失效

## 容器属性
> - flex-direction
> - flex-wrap
> - flex-flow
> - justify-content
> - align-items
> - align-content

### flex-direction属性
> 决定项目排列方向
> 有四个属性的值：
   - row（默认值）：主轴为水平方向，起点在左边
   - row-reverse：主轴为水平方向，起点在右边
   - column：主轴为垂直方向，起点在上方
   - column-reverse：主轴为垂直方向，起点在下方

### flex-wrap属性
> 是否换行
> 有三个属性的值
   - nowrap：不换行
   - wrap：换行，第一行在上方
   - wrap-reverse：换行，第一行在下方

### flex-flow
> 是`flex-direction`和`flex-wrap`的简写形式，默认值为row，nowrap
```js
.box {
  flex-flow: <flex-direction> || <flex-wrap>;
}
```

### justify-content属性
> 定义了项目在主轴上的对齐方式
```js
.box {
  justify-content: flex-start | flex-end | center | space-between | space-around;
}
```
> 有五个属性的值：
   - flex-start（默认值）：左对齐
   - flex-end：右对齐
   - center：居中
   - space-between：两端对齐，项目间隔相等
   - space-around：每个项目两侧间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

### align-items属性
> 定义了项目如何在交叉轴上对齐
```js
.box {
  align-items: flex-start | flex-end | center | baseline | stretch;
}
```
> 有五个属性的值：
   - stretch（默认值）：如果项目未设置高度或者设为auto，将占满整个容器高度
   - flex-start：交叉轴起点对齐
   - flex-end：交叉轴终点对齐
   - center：交叉轴中点对齐
   - baseline：项目第一行文字基线对齐

### align-content属性
> 定义了多跟轴线的对齐方式。如果项目只有一根轴线，那就不起作用
```js
.box {
  align-content: flex-start | flex-end | center | space-between | space-around | stretch;
}
```
> 有五个属性的值：
   - stretch（默认值）：轴线占满整个交叉轴
   - flex-start：与交叉轴起点对齐
   - flex-end：与交叉轴终点对齐
   - center：与交叉轴中点对齐
   - space-between：与交叉轴两端对齐，轴线之间间隔平均分配
   - space-around：每根轴线两侧间隔相等

## 项目属性
> - order
> - flex-grow
> - flex-shrink
> - flex-basis
> - flex
> - align-self

### order属性
> 定义项目的排列顺序：数值越小，排列越靠前，默认为0
```js
.item {
  order: <integer>;
}
```

### flex-grow属性
> 定义项目的放大比例，默认为0，如果存在剩余空间也不放大
```js
.item {
  flex-grow: <number>; /* default 0 */
}
```

### flex-shrink属性
> 定义了项目的缩小比例，默认为1，即如果空间不足，该项目将要缩小

### flex-basis属性
> 属性定义了在分配多余空间之前，项目占据的主轴空间。它可以设为跟width或height属性一样的值（比如350px），则项目将占据固定空间。

### flex属性
> flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。

### align-self属性
> align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。

----------------

# 常见的布局
> - 单列布局
> - 两列自适应布局
> - 三栏布局
> - 粘连布局
> [几种常见的CSS布局](https://juejin.cn/post/6844903710070407182)

## 水平垂直居中
### 行内居中布局
> - 水平居中
>   + 行内元素可设置：text-align: center;
>   + flex布局设置父元素：display: flex; justify-content: center;
>  - 垂直居中
>   + 单行文本父元素确认高度：height === line-height
>   + 多行文本父元素确认高度：disaply: table-cell; vertical-align: middle;

### 块级居中布局
> - 水平居中
>   + 定宽: margin: 0 auto;
>   + 不定宽： 参考上诉例子中不定宽高例子。
>  - 垂直居中
>   + position: absolute设置left、top、margin-left、margin-to(定高)；
>   + position: fixed设置margin: auto(定高)；
>   + display: table-cell；
>   + transform: translate(x, y)；
>   + flex(不定高，不定宽)；
>   + grid(不定高，不定宽)，兼容性相对比较差； 

### 定宽高

#### 绝对定位和负值
```js
<template>
    <div id="app">
        <div class="box">
            <div class="children-box"></div>
        </div>
    </div>
</template>
<style type="text/css">
.box {
    width: 200px;
    height: 200px;
    border: 1px solid red;
    position: relative;
}
.children-box {
    position: absolute;
    width: 100px;
    height: 100px;
    background: yellow;
    left: 50%;
    top: 50%;
    margin-left: -50px;
    margin-top: -50px; 
}
</style>
```

#### 绝对定位 + transform
```js
<template>
    <div id="app">
        <div class="box">
            <div class="children-box"></div>
        </div>
    </div>
</template>
<style type="text/css">
.box {
    width: 200px;
    height: 200px;
    border: 1px solid red;
    position: relative;
}
.children-box {
    position: absolute;
    width: 100px;
    height: 100px;
    background: yellow;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%); 
}
</style>
```

#### 绝对定位 + top/right/bottom/left + margin
```js
<template>
    <div id="app">
        <div class="box">
            <div class="children-box"></div>
        </div>
    </div>
</template>
<style type="text/css">
.box {
    width: 200px;
    height: 200px;
    border: 1px solid red;
    position: relative;
}
.children-box {
    position: absolute;
    display: inline;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: yellow;
    margin: auto;
    height: 100px;
    width: 100px;
}
</style>

```

#### flex布局
```js
<template>
    <div id="app">
        <div class="box">
            <div class="children-box"></div>
        </div>
    </div>
</template>
<style type="text/css">
.box {
    width: 200px;
    height: 200px;
    border: 1px solid red;
    display: flex;
    justify-content: center;
    align-items: center;
}
.children-box {
    background: yellow;
    height: 100px;
    width: 100px;
}
</style>

```

#### grid布局（网格布局）
> 要注意兼容性问题

```js
<template>
    <div id="app">
        <div class="box">
            <div class="children-box"></div>
        </div>
    </div>
</template>
<style type="text/css">
.box {
    width: 200px;
    height: 200px;
    border: 1px solid red;
    display: grid;
}
.children-box {
    width: 100px;
    height: 100px;
    background: yellow;
    margin: auto;
}
</style>

```

### 不定宽高

#### 绝对定位 + transform
```js
<template>
    <div id="app">
        <div class="box">
            <div class="children-box">111111</div>
        </div>
    </div>
</template>
<style type="text/css">
.box {
    width: 200px;
    height: 200px;
    border: 1px solid red;
    position: relative;
}
.children-box {
   position: absolute;
   background: yellow;
   left: 50%;
   top: 50%;
   transform: translate(-50%, -50%);
}
</style>

```

#### table-cell
```js
<template>
    <div id="app">
        <div class="box">
            <div class="children-box">111111</div>
        </div>
    </div>
</template>
<style type="text/css">
.box {
    width: 200px;
    height: 200px;
    border: 1px solid red;
    display: table-cell;
    text-align: center;
    vertical-align: middle;
}
.children-box {
   background: yellow;
   display: inline-block;
}
</style>

```

#### flex布局
```js
<template>
    <div id="app">
        <div class="box">
            <div class="children-box">11111111</div>
        </div>
    </div>
</template>
<style type="text/css">
.box {
    width: 200px;
    height: 200px;
    border: 1px solid red;
    display: flex;
    justify-content: center;
    align-items: center;
}
.children-box {
    background: yellow;
}
</style>

```

#### flex变异布局
```js
<template>
    <div id="app">
        <div class="box">
            <div class="children-box">11111111</div>
        </div>
    </div>
</template>
<style type="text/css">
.box {
    width: 200px;
    height: 200px;
    border: 1px solid red;
    display: flex;
}
.children-box {
    background: yellow;
    margin: auto;
}
</style>

```

#### grid + flex布局
```js
<template>
    <div id="app">
        <div class="box">
            <div class="children-box">11111111</div>
        </div>
    </div>
</template>
<style type="text/css">
.box {
    width: 200px;
    height: 200px;
    border: 1px solid red;
    display: grid;
}
.children-box {
    background: yellow;
    align-self: center;
    justify-self: center;
}
</style>

```

#### grid + margin布局
```js
<template>
    <div id="app">
        <div class="box">
            <div class="children-box">11111111</div>
        </div>
    </div>
</template>
<style type="text/css">
.box {
    width: 200px;
    height: 200px;
    border: 1px solid red;
    display: grid;
}
.children-box {
    background: yellow;
    margin: auto;
}
</style>

```

#### writing-mode属性布局
```js
<template>
    <div id="app">
        <div class="box">
            <div class="children-box">
                <p>11111</p>
            </div>
        </div>
    </div>
</template>
<style type="text/css">
.box {
    width: 200px;
    height: 200px;
    border: 1px solid red;
    writing-mode: vertical-lr;
    text-align: center;
}

.box>.children-box {
    writing-mode: horizontal-tb;
    display: inline-block;
    text-align: center;
    width: 100%;
}

.box>.children-box>p {
    display: inline-block;
    margin: auto;
    text-align: left;
    background: yellow;
}
</style>

```

# 动画实现

## CSS3动画实践
> 常见的CSS3动画一般有补间动画和逐帧动画两种
> [详细介绍](https://jelly.jd.com/article/6006b1025b6c6a01506c8789)
### 补间动画
> 常用于实现位移、颜色(透明度)、大小、旋转、倾斜等变化。一般有`Transitions`和`Keyframes animation`两种方法实现补间动画。
> - Transitions：用于实现简单动画，之后起始两帧过度。多用于页面的交互操作。
>   + CSS的transition允许CSS的属性值在一定的时间区间内平滑地过渡。 这种效果可以在鼠标单击、获得焦点、被点击或对元素任何改变中触发，并圆滑地以动画效果改变CSS的属性值。
> - Keyframes animation：用于实现更复杂的动画，一般关键帧较多
>   + 设置动画关键帧的规则。`animation`的`time-function`设置为`ease`，`linear`或`cubic-bezier`。它会在每个关键帧之间插入补间动画，产生具有连贯性的动画。

### 逐帧动画
> `animation`的`timing-function`默认值为`ease`，它会在每个关键帧之间插入补间动画，所以动画效果是连贯性的。 除了`ease`、`linear`、`cubic-bezier`之类的过渡函数都会为其插入补间。 有些效果不需要补间，只需要关键帧之间的跳跃，这时应该使用`steps`过渡方式。

## CSS3动画性能优化
> 1. 动画中尽量少使用能触发layout和paint的CSS属性，使用更低耗的transform、opacity等属性
> 2. 尽量减少或者固定层的数量，不要在动画过程中创建层
> 3. 尽量减少层的更新（paint）次数

## CSS3动画代替JS动画的好处
> [好处](https://blog.csdn.net/weixin_30532987/article/details/99259744)

--------------

# 盒子模型
> [详细介绍](https://www.cnblogs.com/qianguyihao/p/7256371.html)
## 盒子模型属性
> - **width**：内容的宽度（不是盒子的宽度）
> - **height**：内容的高度（不是盒子的高度）
> - **padding**：内边距
> - **border**：边框
> - **margin**：外边距

## 标准盒子模型与IE和盒子模型的区别
> 在标准盒模型中，`width`和`height`指的是内容区域的宽高，增加内边距，边框和外边距不会对内容产生影响，但会增加元素框总尺寸。
> 在IE盒子模型中，`width`和`height`指的是内容区域的狂傲+`padding`+`border`
