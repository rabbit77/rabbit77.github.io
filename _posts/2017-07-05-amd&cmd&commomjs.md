#  `CommonJs` & `AMD` & `CMD` & `seajs`
1. CommonJs

    在CommonJs中，有一个全局性方法require()，用于加载模块。
    ```
    var math = require('math');
    math.add(2,3);
    ```
    但是在浏览器运行有一个很大的问题，第二行的math.add需要等require执行之后，即math.js模块加载完才能加载完成。模块都放在服务器端，等待的时间取决于网速快慢，可能要等很长时间，浏览器处于‘假死’状态。
    <br/>

    因此，浏览器的模块不能采用'同步加载'，必须采用'异步加载'

2. AMD（Asynchronous Module Define）

    异步模块定义。它采用异步的方式加载模块，模块的加载不影响它后面语句的运行。所有依赖这个模块的语句，都定义在一个回调函数中，等到加载完成之后，这个回调函数才会运行。

    <br/>

    AMD 也采用require()语句加载模块，但不同于CommonJs,它要求两个参数：
    ```
    require([module],callback)
    ```
    第一个参数是[module]，是一个数组，里面的成员就是要加载的模块。第二个参数callback，是加载成功之后的回调函数。

    <br/>
    主要有两个JavaScript库实现了AMD规范，require.js和curl.js

3.  require.js

    解决的问题：
    a. 实现js文件的异步加载，防止网页失去响应
    b. 管理模块之间的依赖性，便于代码的编写和维护

4.  CMD
    依赖就近原则，需要的时候再require
    ```
    define(function(require,exports,module)){
        var clock = require('clock');
        clock.start();
    }
    ```

    <br/>

    AMD 和 CMD 最大的区别是对依赖模块的执行时机处理不同，而不是加载的时机或方式不同，二者皆为异步加载模块。
    AMD依赖前置，js可以方便知道依赖模块是谁，立即加载；而CMD就近依赖，需要使用把模块变为字符串解析一遍才知道依赖了哪些模块。
    <br/>

参考文章 [csdn](http://blog.csdn.net/jackwen110200/article/details/52105493)
