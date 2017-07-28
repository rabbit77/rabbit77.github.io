#  web安全之XSS、CSRF、SQL、JWT

## XSS(跨站脚本攻击)
跨站脚本(cross-site scripting),是一种网站应用程序的安全漏洞攻击，是网络攻击的一种。它允许恶意用户将代码注入到网页中，其它用户在观看网页是会受影响。这类攻击通常包含了HTML及用户端脚本语言。
防御措施：
* 过滤特殊字符
* 使用http头指定类型

## CSRF(跨站请求伪造)

跨站请求伪造（英语：Cross-site request forgery），也被称为 one-click attack 或者 session riding，通常缩写为 CSRF 或者 XSRF， 是一种挟制用户在当前已登录的Web应用程序上执行非本意的操作的攻击方法。
诱导用户去第三方网页
<br/>
跟跨网站脚本（XSS）相比，XSS 利用的是用户对指定网站的信任，CSRF 利用的是网站对用户网页浏览器的信任。
防御措施
<br/>
检查referer字段，Referer check 可以被用于检查是否来自合法的“源”
添加校验token

## SQL注入
用户控制页面输入

## ClickJacking(点击劫持)
透明的iframe
解决办法：禁止iframe的嵌套
