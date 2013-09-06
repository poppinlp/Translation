> 贡献者：梁鹏  
> 翻译时间：2013年9月6日  
> 原文来源：https://github.com/ariya/phantomjs/wiki/Network-Monitoring  
> 原文作者：PhantomJS  
> 原文标题：Network Monitoring  

#网络监测

因为PhantomJS允许查看网络流量，所以它适合用来做各种各样的网络行为和性能分析。

所有资源的请求和响应都能够通过`onResourceRequested`和`onResourceReceived`来嗅探到。一个简单的用来纪录所有请求和响应的例子在[netlog.js](https://github.com/ariya/phantomjs/blob/master/examples/netlog.js)中被使用：

```
var page = require('webpage').create();
page.onResourceRequested = function (request) {
    console.log('Request ' + JSON.stringify(request, undefined, 4));
};
page.onResourceReceived = function (response) {
    console.log('Receive ' + JSON.stringify(response, undefined, 4));
};
page.open(url);
```

通过收集和格式化数据，另一个[netsniff.js](https://github.com/ariya/phantomjs/blob/master/examples/netsniff.js)例子用[HAR格式](http://www.softwareishard.com/blog/har-12-spec)导出了网络流量状况。可以使用[HAR查看工具](http://www.softwareishard.com/blog/har-viewer)来查看结果并获取瀑布流。

下图是BBC网站的瀑布流的例子：

![瀑布流](https://lh6.googleusercontent.com/-xoooH5EB6EE/TgnyJ3r9sRI/AAAAAAAAB98/wYJ_VoWED34/s640/bbc-har.png)

更多高级的网络分析，请看[Confess.js](https://github.com/jamesgpearce/confess)和[YSlow](http://yslow.org/)。

YSlow和PhantomJS的组合对于自动监测网络性能非常实用。报告可以是TAP（Test Anything Protocol）或者JUnit。在诸如Jenkins之类的集成系统里通过PhantomJS运行YSlow，将会很容易的获得一个DIY性能监测方案：

![YSlow](https://a248.e.akamai.net/camo.github.com/81a6855c69c5baeb8020e2873069d733543fda66/687474703a2f2f692e696d6775722e636f6d2f30766a7a512e706e67)
