> 贡献者：梁鹏  
> 翻译时间：2013年8月28日  
> 原文来源：https://github.com/ariya/phantomjs/wiki/Quick-Start  
> 原文作者：PhantomJS
> 原文标题：Quick Start  

#快速入门

本文假设已经安装了PhantomJS，并且PhantomJS的可执行文件在`PATH`路径中。

本文中的代码在[PhantomJS的示例](https://github.com/ariya/phantomjs/wiki/Examples)中都能找到。同时也推荐你去阅读PhantomJS在以下方面的使用：[页面自动化](https://github.com/ariya/phantomjs/wiki/Page-Automation)、[网络监控](https://github.com/ariya/phantomjs/wiki/Network-Monitoring)、[图片截取](https://github.com/ariya/phantomjs/wiki/Screen-Capture)和[headless testing](https://github.com/ariya/phantomjs/wiki/Headless-Testing)。

##Hello World

创建一个包含以下文字的文本文件：

```
console.log('Hello, world!');
phantom.exit();
```

保存成`hello.js`文件，然后在命令行而不是REPL中执行它。

REPL是一种简单的交互式的程序环境。更多关于REPL的信息请阅读[这篇文章](https://github.com/ariya/phantomjs/wiki/REPL)。再次强调，REPL是可执行程序phantomjs.exe而不是命令行。

在命令行中执行如下的语句：

```
phantomjs hello.js
```

看到的输出结果为

> Hello, world!

在代码的第一行，`console.log`将文字输出到终端。在代码的第二行，`phantom.exit`会终止程序的执行。

在程序中的某个地方调用`phantom.exit`来结束执行__非常重要__，如果不这么做的话，PhantomJS程序将不会终止。

##页面加载

可以通过建立一个page对象来堆网页进行加载、解析和渲染。

下面的代码演示了page对象简单的使用方法。它加载了example.com页面，然后把它保存成了`example.png`图片。

```
var page = require('webpage').create();
page.open('http://example.com', function () {
    page.render('example.png');
    phantom.exit();
});
```

正因为渲染功能，PhantomJS能被用来[截取网页](https://github.com/ariya/phantomjs/wiki/Screen-Capture)，本质上是对内容的接图。

下面的`loadspeed.js`脚本加载一个制定的URL（不要忘记HTTP协议）并且统计加载消耗的时间。

```
var page = require('webpage').create(),
    system = require('system'),
    t, address;

if (system.args.length === 1) {
    console.log('Usage: loadspeed.js <some URL>');
    phantom.exit();
}

t = Date.now();
address = system.args[1];
page.open(address, function (status) {
    if (status !== 'success') {
        console.log('FAIL to load the address');
    } else {
        t = Date.now() - t;
        console.log('Loading time ' + t + ' msec');
    }
    phantom.exit();
});
```

在命令行中执行这个脚本：

```
phantomjs loadspeed.js http://www.google.com
```

输出类似下面这样的内容：

> Loading http://www.google.com Loading time 719 msec

##代码评估

可以使用`evaluate()`函数在网页的上下文中来评估Javascript或者Coffeescript代码。这种评估是沙盒式的，它不允许代码去操作任何自己页面上下文之外的Javascript对象和变量。`evaluate()`将返回一个对象，但是只能是个简单的对象，不能包含函数和必包。

这是一个显示网页标题的例子：

```
var page = require('webpage').create();
page.open(url, function (status) {
    var title = page.evaluate(function () {
        return document.title;
    });
    console.log('Page title is ' + title);
});
```

任何来自网页以及`evaluate()`的信息输出默认都不会被显示。可以使用`onConsoleMessage`这个回调来改变这种方式。上面的例子能被改写为：

```
var page = require('webpage').create();
page.onConsoleMessage = function (msg) {
    console.log('Page title is ' + msg);
};
page.open(url, function (status) {
    page.evaluate(function () {
        console.log(document.title);
    });
});
```

因为脚本代码就像在浏览器中一样执行，所以标准的DOM和CSS操作都能执行。这使得PhantomJS能够适应众多的[页面自动化任务](https://github.com/ariya/phantomjs/wiki/Page-Automation)。

##网络请求和响应

当一个页面请求一个远程服务器上的资源时，请求和响应可以通过`onResourceRequested`和`onResourceReceived`回调来跟踪。在[netlog.js](https://github.com/ariya/phantomjs/blob/master/examples/netlog.js)例子中有如下的演示：

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

关于如何使用HAR导出信息给基于YSlow的性能分析工具来使用，更多的信息请看[这个页面](https://github.com/ariya/phantomjs/wiki/Network-Monitoring)。
