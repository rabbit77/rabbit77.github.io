---
layout: default
title: 个人总结
tags: [总结]
---
<br/>
#   以下为之前遇到的bug
<br/>
##   一、img标签src为空引发两次请求页面的问题
<br/>
```html
<img src="">
```
<br/>
在金融项目里，有个页面因为后台返回的图片数据为空，导致页面向后台请求两次接口。<br/>
在这里问题比较严重，每向后台请求一次接口，就会生成一个订单。<br/>
[原理](http://blog.csdn.net/chengmodelong/article/details/44618435)    <br/>
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

##   二、<img> 标签没有before跟after伪元素吗？

*  写一个样式，img标签的伪元素死活出不来。
*  也有一些人认为before跟after作为dom元素，是在容器内渲染的，首先这个容器得可以包含其他元素，input标签及img标签本身都不能包含其他元素，因此不能加before跟after标签

[伪元素伪类--掘金](https://mp.weixin.qq.com/s?__biz=MzI0MDYzOTEyOA==&mid=2247483704&idx=1&sn=ebba5365768889245ca4185b0f011ddc&chksm=e9168ccfde6105d92f9fce14ae201263758e5be70d9500fb89e9dd6c8c71b2c57cf7ae62923f&scene=38#wechat_redirect)

<br/>
##   三、设置before跟after的content
```html
   <div class="pic-content third-pic" data-count="<?= num?>">
```
<br/>

```sass
.third-pic::before {
    content: attr(data-count);
}
```
<br/>
![example](/static/image/tell.png)
<br/>
##   四、location.replace()
调用location.replace()方法后，当前页面不会保存到会话历史中（session History），这样用户点击回退按钮将不会再跳转到该页面。<br/>
这个方法可以解决在APP里，打开按钮跳到前一个页面，这种在APP里按回退按钮无限循环的问题。<br/>
```javascript
location.replace('/activity/logo-answer?question_id=' + self.state.question_id + '&token=' + self.state.token);
```
<br/>
举个简单的栗子
<br/>
##   五、md5
```javascript
import Crypto from 'crypto'

Crypto.createHash('md5').update(string).digest('hex')
```

<br/>
##   六、手机端边框1像素样式
<br/>
```sass
.advisory {
    width: 1.5rem;
    height: .5rem;
    color: @blue;
    text-align: center;
    font-weight: 200;
    line-height: .54rem;
    position: relative;
    &::before{
        border: 1px solid @blue;
        border-radius: .1rem;
        -webkit-transform:scale(0.5);
        transform: scale(0.5);
        position: absolute;
        top: -52%;
        left: -52%;
        content: '';
        width: 200%;
        height: 200%;
    }
}
```
![1像素边框示意图](/static/image/border.png)
<br/>
> 图左是用上述scale(0.5)的方法做出来的效果，图右没有用scale，直接设置border:1px;
> 图右在手机端显示的效果是1px。如果设置为0.01rem，在border就不见了。所以用伪元素结合scale是比较好的解决方案。

<br/>

##  七、JSON.stringify()
<br/>
1. 后台没办法返数据，也不能从localStorage里取，只能自己拼接到链接上。
```html
<%
    var params = {
        type: 'history',
        name: name,
        tel: tel,
        id: identity,
        cid: ele.card_no
    };
%>
<a href="<%=url%>?status=<%=status%>&params=<%= JSON.stringify(params) %>&invalidate_reason=<%= ele.invalidate_reason%>" class="result"></a>
```

2. 向后台发送数据的时候
<br/>
![发送数据截图](/static/image/net.png)

<br/>
##  八、微信二次分享测试  
<br/>
```javascript
wxShare: function() {
            // 微信分享
            if (XIN.platform.wx) {
                var data = {
                    title: shareData.title + ' - 优信新车',
                    desc: shareData.content,
                    link: shareData.url,
                    imgUrl: shareData.icon,
                    success: function() {
                        statistic.pv('statistic/activity_logo_share1_success');
                    }
                }
                share2wx(data)
            }
        }
```

需配置本机域名及端口 80
端口配置方法
```javascript
sudo PORT=80 npm start

PORT=80 npm start
```
<br/>
##  九、jekyll
<br/>
* [jekyll中文官网](http://jekyll.com.cn/)
* [jekyll官网](http://jekyll.com.cn/)
* [利用github和jekyll搭建免费的个人blog](http://damoqiongqiu.github.io/jekyll/2017/07/02/%E5%88%A9%E7%94%A8github%E5%92%8Cjekyll%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BABlog-1.html)
* [搭建一个免费的，无限流量的Blog----github Pages和Jekyll入门--阮一峰博客](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)
* 模板 😳😳😳
<br/>
##  十、setTimeout除了做定时器还能做什么？
setTimeout(fn,0);
<br/>
非常多，比如说：在处理DOM点击事件的时候通常会产生冒泡，<br/>
正常情况下首先触发的是子元素的handler，再触发父元素的handler，<br/>
如果我想让父元素的handler先于子元素的handler执行应该怎么办？<br/>
那就用setTimeout延迟子元素handler若干个毫秒执行吧。问题是这个“若干个”毫秒应该是多少？可以是0<br/>
<br/>
比如下面这个栗子
<br/>
```javascript
(function () {
    setTimeout(function () {
        alert(2);
    }, 0);

    alert(1);
})()
```
<br/>
就会先弹出1
<br/>
原因：setTimeout，setInterval都存在一个最小延迟的问题，虽然你给的delay值为0，但是浏览器执行的是自己的最小值。HTML5标准是4ms，但并不意味着所有浏览器都会遵循这个标准，包括手机浏览器在内，这个最小值既有可能小于4ms也有可能大于4ms。在标准中，如果在setTimeout中嵌套一个setTimeout, 那么嵌套的setTimeout的最小延迟为10ms。
<br/>
参考文章：[你真的了解setTimeout和setInterval吗？](http://qingbob.com/difference-between-settimeout-setinterval/)
<br/>
##  十一、分享几道有意思的js面试题
[几道有意思的js面试题--from eplover's blog](https://eplover.github.io/pages/2017/03/17/interest-questions.html)
<br/>
<br/>
