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
##   二、点击鼠标提交form表单的数据
<br/>
按钮放在form表单里点击会引起当前页面刷新<br/>
demo<br/>
<form>
<button>button1</button>
<button>button2</button>
<button>button3</button>
</form>
<br/>
##   三、<img> 标签没有before跟after伪元素吗？
    *  写一个样式，img标签的伪元素死活出不来。已经排除是不是块级元素影响，因为mdn上给出的例子，span可以有伪元素
    *  也有一些人认为before跟after作为dom元素，是在容器内渲染的，首先这个容器得可以包含其他元素，input标签及img标签本身都不能包含其他元素，因此不能加before跟after标签

<br/>
##   四、设置before跟after的content
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
##   五、location.replace()
调用location.replace()方法后，用户就不能回到前一个页面。<br/>
这个方法可以很好的解决在APP里，打开按钮跳到前一个页面，这种在APP里按回退按钮无限循环的问题。<br/>
```javascript
location.replace('/activity/logo-answer?question_id=' + self.state.question_id + '&token=' + self.state.token);
```
<br/>
##   六、md5
```javascript
import Crypto from 'crypto'

Crypto.createHash('md5').update(string).digest('hex')
```

<br/>
##   七、手机端边框1像素样式
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

##  八、JSON.stringify()
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
##  九、微信二次分享测试  
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
```
<br/>
##  十、jekyll
<br/>
* [jekyll中文官网](http://jekyll.com.cn/)
* [jekyll官网](http://jekyll.com.cn/)
* [搭建一个免费的，无限流量的Blog----github Pages和Jekyll入门--阮一峰博客](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)
* 模板 😳😳😳


<br/>
<br/>
<br/>
