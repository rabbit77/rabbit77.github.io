## 前端知识汇总
1. Doctype的作用？标准模式与兼容模式有何区别？
> 1. <!Doctype>声明位于HTML文档的第一行，处于<html>标签之前，告知浏览器的解析器用什么文档标准解析这个文档，doctype不存在或者错误会导致文档以兼容模式出现。
> 2. 标准模式的排版和JS运作模式都是以该浏览器支持的最高标准。在兼容模式中，页面以宽松的向后兼容的方式显示，模拟老式浏览器防止站点无法工作。

2. 行内元素有哪些？块级元素有哪些？空元素有哪些？
> 每个元素都有display属性，确定该元素的类型，每个元素都有默认的display值
> 1） 行内元素有 a b span img input select strong
> 2)  块级元素  div ul ol li dl dt dd h1 .. h6 p
> 3)  常见的空元素  
>     <br>  <hr>(创建一条水平线) <img> <input> <link> <meta>
>   鲜为人知的是：
  	<area> <base> <col> <command> <embed> <keygen> <param> <source> <track> <wbr>

3. 页面导入样式时，使用link和@import的区别
* link属于XHTML标签，除了加载CSS外，还能用于定义RSS，定义rel连接属性等作用；而@import是css定义的，只能加载css
* 页面被加载时，link会被同时加载，而@import引用的css会等页面加载完再加载
* import是css2.1提出的，只有IE5以上才能识别；link无兼容性问题
4. 介绍下对浏览器内核的理解
* 主要分为两部分：渲染引擎和JS引擎
* 渲染引擎负责取得网页的内容（HTML、XML、图像等）、整理讯息（加入CSS等），以及计算网页的显示方式，然后输出至显示器或打印机
* JS引擎：解析和执行JavaScript来实现网页的动态效果

4. 常见的浏览器内核有哪些
* Trident内核：IE,MaxThon,TT,The World,360,搜狗浏览器等。[又称MSHTML]
* Gecko内核：Netscape6及以上版本，FF,MozillaSuite/SeaMonkey等
* Presto内核：Opera7及以上。      [Opera内核原为：Presto，现为：Blink;]
* Webkit内核：Safari,Chrome等。   [ Chrome的：Blink（WebKit的分支）]

5. html5有哪些新特性、移除了那些元素？如何处理HTML5新标签的浏览器兼容问题？如何区分 HTML 和 HTML5？
* HTML5 现在已经不是 SGML 的子集，主要是关于图像，位置，存储，多任务等功能的增加。
  	  绘画 canvas;
  	  用于媒介回放的 video 和 audio 元素;
  	  本地离线存储 localStorage 长期存储数据，浏览器关闭后数据不丢失;
        sessionStorage 的数据在浏览器关闭后自动删除;
  	  语意化更好的内容元素，比如 article、footer、header、nav、section;
  	  表单控件，calendar、date、time、email、url、search;
  	  新的技术webworker, websocket, Geolocation;

    移除的元素：
  	  纯表现的元素：basefont，big，center，font, s，strike，tt，u;
  	  对可用性产生负面影响的元素：frame，frameset，noframes；
* 支持HTML5新标签：
  	 IE8/IE7/IE6支持通过document.createElement方法产生的标签，
    	 可以利用这一特性让这些浏览器支持HTML5新标签，
    	 浏览器支持新标签后，还需要添加标签默认的样式。

       当然也可以直接使用成熟的框架、比如html5shim;
  	 <!--[if lt IE 9]>
  		<script> src="http://html5shim.googlecode.com/svn/trunk/html5.js"</script>
  	 <![endif]-->

* 如何区分HTML5： DOCTYPE声明|新增的结构元素|功能元素
* html5相关扩展
###  与类相关的扩充
1.  为了让开发人员适应并增加对class属性的新认识，html5新增了许多API，致力于简化css类的用法
*  getElementsByClassName()
*  classList 属性
    add(value)
    contains(value)
    remove(value)
    toggle(value)
###  焦点管理
辅助管理DOM焦点的功能
*  document.activeElement 始终会引用DOM中当前获得了焦点的元素。
*  document.hasFocus() 用于确定文档是否获得了焦点
###  HTMLDocument变化
*  document.readyState属性
    loading:正在加载文档；
    complete,已经加载完文档
* document.head 属性引用文档的<head>元素，作为对document.body引用文档的<body>元素的补充
###  字符集属性
charset
###  自定义数据属性
可以为元素添加非标准的属性，需要加前缀data-
###  插入标记
innerHTML 属性返回与调用元素的所有子节点

6. 简述对html语义化的理解
*  用正确的标签做正确的事情
*  html语义化让页面的内容结构化，结构更清晰，便于对浏览器、搜索引擎🔍解析
*  即使在没有css情况下也以一种文档格式展示，并且是容易阅读的；
*  搜索引擎🔍的爬虫也依赖于HTML标记来确定上下文和各个关键字的权重，利于SEO；
*  使阅读源代码的人对网站更容易将网站分块，便于将来维护

7. html5的离线存储怎么使用，工作原理能不能解释一下？
* 在用户没有与因特网连接时，可以正常访问站点或应用。在用户与因特网连接时，更新用户机器上的缓存文件。
* 原理：html5的离线存储是基于一个新建的.appcache文件的缓存机制，通过这个文件上的解析清单离线存储资源，这些资源就会像cookie一样被存储了下来，之后当网络处于离线状态时，浏览器会通过被离线存储的数据进行页面展示。
* 如何使用
* 在页面头部像下面加入manifest的属性；
* 在cache.manifest文件的编写离线离线存储的资源
* CACHE MANIFEST
  	#v0.11
  	CACHE:
  	js/app.js
  	css/style.css
  	NETWORK:
  	resourse/logo.png
  	FALLBACK:
  	/ /offline.html
* 在离线状态时，操作window.applicationCache进行需求实现

8. 浏览器是怎么对HTML5的离线储存资源进行管理和加载的呢？
> 在线的情况下，浏览器发现html头部有manifest属性，它会请求manifest文件，如果是第一次访问app，那么浏览器就会根据manifest文件的内容下载相应的资源并且进行离线存储。如果已经访问过app并且资源已经离线存储了，那么浏览器就会使用离线的资源加载页面，然后浏览器会对比新的manifest文件与旧的manifest文件，如果文件没有发生改变，就不做任何操作，如果文件改变了，那么就会重新下载文件中的资源并进行离线存储。
离线的情况下，浏览器就直接使用离线存储的资源。

9. 描述cookie、sessionStorage、localStorage的区别
* cookie 是为了标识用户信息而存储在用户本地终端上的数据
* cookie数据始终在同源的http请求中携带（即使不需要），即会在浏览器和服务器间来回传递
* sessionStorage和localStorage不会自动把数据发送给服务器，仅存储在本地
#### 存储大小
* cookie数据不能超过4k，sessionStorage和localStorage可以达到5M或更大。
#### 有效时间
* localStorage 存储持久数据，浏览器关闭后数据不丢失，除非主动删除数据
* sessionStorage 数据在当前浏览器窗口关闭后自动删除
* cookie 设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭

10. iframe有哪些缺点
* iframe会阻塞主页面的onload事件；
* 搜索引擎🔍的检索程序无法解读这种页面，不利于SEO；

11. label的作用是什么❓是怎么用的
* label标签来定义表单控件间的关系，当用户选择该标签时，浏览器会自动将焦点跳转到和标签相关的表单控件上
    ```
    <label for="Name">Number:</label>
    <input type="text" name="Name" id="Name"/>
    <label>Date:<input type="text" name="B"/></label>
    ```
12. HTML5的form如何关闭自动完成功能？

autocomplete=off

13. 如何实现浏览器内多个标签页之间的通信？（阿里）
LocalStorage、cookie
websocket、shareworker

14. websocket如何兼容低版本浏览器？（阿里）
adobe flash socket;
activeX HTMLFile;
基于`multipart`编码发送`XHR`
基于长轮询的`XHR`

15. 页面可见性（Page Visibility API）可以有哪些用途
通过`VisibilityState`的值检测页面当前是否可见，以及打开网页的时间等；
在页面被切换到其他后台进程时，自动暂停音乐🎵或视频播放；

16. 如何在页面上实现一个圆形的可点击区域？
*  map+area 或 `svg`
*  border-radius
*  纯js实现，需要求一个点在不在圆上的简单算法、获取鼠标坐标等等

17. 网页验证码是干嘛用的，是为了解决什么安全问题？
* 区分用户是计算机还是人的公共全自动程序，可以防止恶意破解密码、刷票、论坛灌水；
* 有效防止黑客对某一特定注册用户用特定程序暴力破解的方式进行不断地登录尝试。
*

18. overflow:scroll;在页面上卡顿的问题
```
{
    overflow:scroll;
    -webkit-overlow-scrolling:touch;
}
```
开启硬件加速
