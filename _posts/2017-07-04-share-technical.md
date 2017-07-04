---
layout: post
title: 个人总结
tags: [总结]
---
#  以下为之前项目中遇到的一些小bug

##  img标签src为空引发两次请求页面的问题

```html
<img src="">
```
在金融项目里，有个页面因为后台返回的图片数据为空，导致页面向后台请求两次接口。 在这里问题比较严重，每向后台请求一次接口，就会生成一个订单。

解决办法：
* 设置缺省图

```html
<img src="<%= v.pic.pic_url %>" onerror="this.onerror=null;this.src='//c4.xinstatic.com/che/20161109/1820/5822f87620d71845964.jpg';">
```

## 点击鼠标提交form表单的数据
