> 贡献者：PoppinLp  
> 翻译时间：2013年9月4日  
> 原文来源：https://github.com/ariya/phantomjs/wiki/Inter-Process-Communication  
> 原文作者：PhantomJS  
> 原文标题：Inter Process Communication  

#进程间通信

在PhantomJS和其他进程之间，有很多方法来实现进程间的通信。

##文件输入输出

* [PhantomJS File API](https://github.com/ariya/phantomjs/wiki/API-Reference-FileSystem)
* 套接字
* 命名管道

##HTTP

* 发送给外部的HTTP请求
    * 提供给服务器端的GET/POST数据
    * 提供给服务器端的GET/POST数据，结果返回JSON/XML/HTML等
    * 创建一个XMLHttpRequest对象，然后像在通常网页中一样使用它
    * 跨域请求默认是被禁止的。请在服务器上使用[`Access-Control-Allow-Origin`](http://www.w3.org/TR/cors/#access-control-allow-origin-response-header)来开启。
* 来自外部的HTTP请求，使用[PhantomJS WebServer API](https://github.com/ariya/phantomjs/wiki/API-Reference-WebServer)。
* 使用[mitmproxy/libmproxy](http://mitmproxy.org/)或者[fiddler](http://fiddler2.com/)之类的HTTPS代理来路由。

##网页上下文中的网络套接字

* [hixie-76](http://tools.ietf.org/html/draft-hixie-thewebsocketprotocol-76)网络套接字
* PhantomJS 2.x支持[RFC 6455](http://tools.ietf.org/html/rfc6455)网络套接字

##标准输入流、输出流、错误流

详情请看这个例子[stdin-stdout-stderr.js](https://github.com/ariya/phantomjs/blob/master/examples/stdin-stdout-stderr.js)
