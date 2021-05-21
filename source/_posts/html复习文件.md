---
title: HTML复习
date: 2021-05-19 16:46:51
categories:
 - 前端
 - HTML
tags:
 - 前端
 - HTML

---
工作这么久了，框架用的太多，基础知识都忘记了，按照网上的面试题整理一下。<del>(才不会说是我太笨了)</del>
<!-- more -->

-------------
 # 标签语义化
  > **意义：**在适当的内容使用适当的标签.
  **优点：**利于SEO优化，方便搜索引擎的爬虫抓取有效信息。支持读屏软件，可以根据文章自动生成目录，对开发者友好，语义化标签便于开发和维护.
  **常见的语义化标签：** `<header>` `<nav>` `<section>` `<main>` `<artical>` `<aside>` `<footer>`
  
-----------

 # DOCTYPE(⽂档类型)的作⽤
  > 目的：是H5中一种通用标记语言的文档类型声明，目的是为了以什么样的文档类型(html.xhtml)来解析文档
-----------

 # script标签中defer和async的区别
   > 如果没有`defer`或者`async`的话，浏览器会立即加载并执行脚本，意思就是不等待后续加载的文档元素，读到就开始执行，这样会阻塞后续文档的加载
   
   > **defer和async区别**
   > 1. 带有async属性的标签不能保证加载顺序，多个带有defer的标签，按照加载顺序执行
   > 2. async属性表示后续文档的加载和执行与js脚本的加载和执行是并行的
   > 3. defer属性表示后续文档的加载和js脚本加载是并行的，但是js脚本的执行要等到文档解析完成之后，DOMContentLoaded事件触发执行之前
-----------

 # meta标签
 ## 常用的meta标签
  > - **`<meta charset="UTF-8" >`** 表示html文档的编码类型
  > - **`<meta name="keywords" content="关键词" />`** 表示html文档的关键词
  > - **`<meta name="description" content="页面描述" />`** 表示html文档的页面描述
  > - **`<meta name="refresh" content="0;url" />`** 表示html文档的页面重定向和刷新
  > - **`<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1" />`** 适配移动端，开发人员可以控制视口的大小和比例

## content的参数
> - `width`, `height`, `initial-scale(初始缩放比例)`, `maximum-scale(最大缩放比例)`, `minimum-scale(最小缩放比例)`, `user-scalable(是否允许用户缩放)`
> - <meta name="robots" content="index,follow" /> 搜索引擎方式 
> - `content`的参数
> - `all`(文件将被检索，且页面上的链接可以被查询)
> - `none`(文件将不会检索，且页面上的链接不可以被查询)
> - `index`(文件将被检索)
> - `follow`(页面上的链接可以被查询)
> - `noindex`(文件将不被检索)
> - `nofollow`(页面上的链接不可以被查询)
-----------

 # HTML5更新内容
 ## 语义化标签
 ## 媒体标签
 1. `audio(音频)` 
 ```js
     <audio src='' controls autoplay loop='true'></audio>
 ```
 2. `属性：`controls 控制面板 autoplay 自动播放 loop='true'循环播放
 3. `video(视频)`
 ```js
 <video src='' poster='imgs/aa.jpg' controls></video>
 <video>
 	<source src='aa.flv' type='video/flv'></source>
 	<source src='aa.mp4' type='video/mp4'></source>
 </video>
 ```
 4. `表单`
 5. `进度条，度量器`
 6. `DOM查询操作`
 7. `Web存储`
 8. `其他`
-----------

# display:block display:inline display:inline-block区别
  > 1. **`block：`** 独占一行，多个元素会另起一行，可以设置`width`，`height` `margin`和`padding`属性
  2. **`inline：`** 不会独占一行，设置`width`，`height`无效，可以设置水平方向的`margin`和`padding`,不可以设置垂直方向的`margin`和`padding`
  3. **`inline-block：`** 将对象设置为`inline`对象，但对象内容作为`block`对象呈现
-----------

 # HTML5离线存储怎么使用，原理是什么
 > 离线存储指的是用户没有网络连接时，可以正常访问站点或应用，在用户网络连接时，更新缓存文件

 ## 原理
 > `HTML5`的离线存储是基于一个新建的`.appcache`文件的缓存机制，通过这个文件上的解析清单离线存储资源，这些资源就会像`cookie`一样缓存下来。之后如果网络处于离线状态，就会通过被离线存储的数据进行页面展示。
 ### 使用方法
 > 1. 创建一个和`html`同名的`manifest='index.mainifest'`,在页面头部下方加入`mainifest`的属性
   2. 在`cache.manifest`文件下编写离线存储的资源
   ```js
   CACHE MANIFEST
    #v0.11
    CACHE:
    js/app.js
    css/style.css
    NETWORK:
    resourse/logo.png
    FALLBACK:
    / /offline.html
   ```
   3. 在离线状态，操作`window.applicationCache` 进行离线缓存

### 解释   
> - `CACHE：`需要离线缓存的资源列表，由于包含mainifest文件页面的将被自动存储下来，所以不需要把页面自身也放入列表
> - `NETWORK：`表示在他下面的资源只有在在线情况才能访问，他们不会被离线存储，所以离线情况下无法使用这些资源。如果在`CACHE`和`NETWORK`中有同一个资源，那它还是会被缓存，说明`CACHE`的优先级更高
> - `FALLBACK：`如果访问第一个资源失败了，就去访问`FALLBACK`的资源
## 如何更新缓存
> （1）更新`mainifest`文件
（2）通过`javascript`进行操作
（3）清除浏览器缓存
## 注意事项
> （1）每个浏览器的缓存大小不一样（浏览器设置的大小为5MB）
（2）如果`mainifest`文件，或内部列举的某一个文件下载失败，那整个更新过程都失败，浏览器继续使用老的缓存。
（3）引用`mainifest`的`html`必须与`mainifest`文件同源
（4）`FALLBACK`的文件必须与`mainifest`文件同源
（5）当一个资源被缓存后，该浏览器直接访问这个绝对路径也会访问缓存中的资源
（6）站点中的其他页面即使没有设置`mainifest`属性，请求资源如果在缓存中也会从缓中访问
（7）当`mainifest`文件发生改变时，资源请求本身也会触发更新

-----------

# 浏览器怎么对HTML5离线缓存资源进行管理和加载
> - 网络在线的情况下，浏览器发现`html`头部有`mainifest`属性，他会请求`mainifest`文件，如果是第一次访问，那浏览器会根据`mainifest`的文件内容下载相应资源并缓存。如果已经访问过app并进行了离线缓存，那浏览器直接使用离线资源加载页面，然后对比新的mainifest文件和旧的mainifest文件，如果没有改变，不更新，如果新版有改变就重新下载mainifest文件中的资源并进行离线缓存
> - 网络如果离线，直接使用离线存储资源
-----------

 # title与h1的区别，b与strong的区别，i与em的区别
 > - `title`没有明确意义，只是一个标题。`h1`表示层次分明标题，对页面信息的抓取也有很大影响
 > - `strong`标明重点内容，有语气加强的含义，使用设备阅读时候会重读。而`b`是展示强调内容
 > - `i`内容展示为斜体，`em`表示强调的文本
 -----------

 # iframe有哪些优点和缺点
 > - `iframe`元素会创建包含另一个文档的内联框架
 - 优点：
 > 1. 可以用来加载比较慢的内容（例如广告）
 > 2. 可以是脚本进行并行下载
 > 3. 可以实现跨子域通信
 - 缺点：
 > 1. `iframe`会阻塞页面的onload事件
 > 2. 无法被一些搜索引擎识别
 > 3. 会产生很多页面，不方便管理
-----------

# label的作用是什么？怎么用？
 > - `label`用来控制表单控件关系，当用户选择`label`标签时，浏览器自动将焦点转到，`label`和`label`相关的表单控件上
  ```
  <label for="mobile">Number:</label>
  <input type="text" id="mobile"/>
  ```
-----------

# Canvas和SVG有什么区别？
 > - **`Canvas`** 是通过`js`来绘制2d图形的方法。是通过逐像素来进行渲染的，当我们对`Canvas`进行缩放时，会出现图片锯齿或失真的情况
 > - **`SVG`** 是一种通过XML来描述2D图形的语言。`SVG`寄予XML，这意味着`SVG DOM`中的每一个元素都是可用的，可以为某个元素附加监听事件。并且`SVG`保存的是图片的绘制方法，所以当图片缩放时，并不会失真。
------------

# head中必不可少的标签是？
 > - 标签用于定义文档头部，是所有头部信息的容器。里面包含了各种属性和信息，包括文档的标题、在Web中得位置以及和其他文档的关系，绝大多数头部信息都不会作为信息展示给读者。
 > - 文档中的可用标签为`<base>`, `<link>`, `<meta>`, `<script>`, `<style>`, `<title>`。
 > - 其中`<title>` 定义文档的标题，它是head部分中唯一必需的元素。
