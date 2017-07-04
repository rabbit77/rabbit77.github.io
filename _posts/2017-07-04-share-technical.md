---
layout: default
title: 个人总结
tags: [总结]
---
<br/>
#   以下为之前遇到的bug
<br/>
###   一、img标签src为空引发两次请求页面的问题
<br/>
```html
<img src="">
```
<br/>
在金融项目里，有个页面因为后台返回的图片数据为空，导致页面向后台请求两次接口。/r/n
在这里问题比较严重，每向后台请求一次接口，就会生成一个订单。

解决办法：
 * 设置缺省图
<br/>
```html
<img src="<%= v.pic.pic_url %>" onerror="this.onerror=null;this.src='//c4.xinstatic.com/che/20161109/1820/5822f87620d71845964.jpg';">
```
<br/>
不过需要注意的是在JavaScript里引用的ejs模板里用onerror方法，页面会报错
```html                           
<img src="<?= lists.header_pic?>" onerror="this.onerror=null; this.src='//c4.xinstatic.com/f1/20170322/1037/58d1e36350971261856.jpg';" alt="车型图">
```
> 报错信息会提示语法错误，missing ) ，这个提示在很大程度上给排除bug造成了误解。
<br/>
###   二、点击鼠标提交form表单的数据
<br/>
###   三、<img> 标签没有before跟after伪元素吗？
    写一个样式，img标签的伪元素死活出不来，而加在section标签上立马就出来了。已经排除是不是块级元素影响，因为mdn上给出的例子，span可以有伪元素
    * 也有一些人认为before跟after作为dom元素，是在容器内渲染的，首先这个容器得可以包含其他元素，input标签及img标签本身都不能包含其他元素，因此不能加before跟after标签

<br/>
###   四、设置before跟after的content
.third-pic::before {
    content: attr(data-count);}
<br/>
###   五、其实重点想说的是location.replace()方法，调用replace()方法后，用户就不能回到前一个页面。这个方法可以很好的解决在APP里，打开按钮跳到前一个页面，这种在APP里按回退按钮无限循环的问题
<br/>
###   六、元素设置width:100%; padding: 0 .35rem; 想实现左右两边空出来一定距离。但是这样的话，右边就出去了。这时候只要把width:100%去掉就好了。
    单纯设置overflow是不管用的。
<br/>
