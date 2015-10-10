> 贡献者：PoppinLp  
> 翻译时间：2014年4月20日  
> 原文来源：https://http://phantomjs.org/api/phantom/  
> 原文作者：PhantomJS  
> 原文标题：phantom Object  

#phantom Object
各种PhantomJS的功能现在被封装到了一个叫`phantom`的新的宿主对象，该对象是[`window`对象](https://developer.mozilla.org/en/DOM/window)的子对象。

##属性

###args
`phantom.args` {String[]}

稳定性：__不推荐使用__ - 推荐使用[System模块](https://github.com/poppinlp/Lranslation/edit/master/phantomJS/system.md)的[`system.args`](https://github.com/poppinlp/Lranslation/edit/master/phantomJS/system.md#args)

该属性只读，是传递给脚本的参数数组。

###cookies
`phantom.cookies` {Object[]}

PhantomJS 1.7开始支持

可以对任何域名获取或者设置Cookie（尽管如此，对于设置Cookie，还是推荐使用[`phantom.addCookie`](https://github.com/poppinlp/Lranslation/edit/master/phantomJS/phantom-object.md#addcookie)）。这些Cookies储存在CookieJar中，在打开相关的网页时会被使用。

如果PhantomJS[启动配置](http://phantomjs.org/api/command-line.html)中指定的cookie文件里存在Cookie数据，那么那些数据将会被提前放入这个数组中。

###cookiesEnabled
`phantom.cookiesEnabled` {Boolean}

PhantomJS 1.7开始支持

控制CookieJar是否启用。默认为`true`。

###libraryPath
`phantom.libraryPath` {String}

这个属性储存着[`injectJs`](https://github.com/poppinlp/Lranslation/edit/master/phantomJS/phantom-object.md#injectjs)方法使用的用来解析脚本名称的路径。它的初始值为PhantomJS执行的脚本所在的目录。

###scriptName
`phantom.scriptName` {String}

稳定性：__不推荐使用__ - 推荐使用[System模块](https://github.com/poppinlp/Lranslation/edit/master/phantomJS/system.md)的[`system.args[0]`](https://github.com/poppinlp/Lranslation/edit/master/phantomJS/system.md#args)

该属性只读，是当前执行的脚本文件名。

###version
`phantom.version` {Object}

该属性只读，是当前的PhantomJS版本信息。例如`{ 'major': 1, 'minor': 9, 'patch': 7}`。

##方法

###addCookie
`phantom.addCookie(Object)` {Boolean}

PhantomJS 1.7开始支持

将一个Cookie加入CookieJar。添加成功返回`true`，否则返回`false`。

例子：
```
phantom.addCookie({
    'name': 'Added-Cookie-Name',
    'value': 'Added-Cookie-Value',
    'domain': '.google.com'
});
```

###clearCookies
`phantom.clearCookies()` {void}

PhantomJS 1.7开始支持

删除CookieJar中所有的Cookie。

###deleteCookie
`phantom.deleteCookie(cookieName)` {Boolean}

PhantomJS 1.7开始支持

删除CookieJar中`name`属性为`cookieName`的Cookie。删除成功返回`true`，否则返回`false`。

例子：

```
phantom.deleteCookie('Added-Cookie-Name');
```

###exit
`phantom.exit(returnValue)` {void}

返回给定的返回值并结束当前程序。如果没有设置返回值，默认返回0。

例子：

```
if (somethingIsWrong) {
    throw new Error('myProject.something failed to locate whatever.etc');
    phantom.exit(1);
} else {
    phantom.exit(0);
}
```

###injectJs
`phantom.injectJs(filename)` {Boolean}

从指定的文件注入外部脚本代码到Phantom。如果在当前目录中找不到该文件，会在[`libraryPath`](https://github.com/poppinlp/Lranslation/edit/master/phantomJS/phantom-object.md#librarypath)指定的路径中去寻找。如果注入成功返回`true`，否则返回`false`。

例子：

```
var wasSuccessful = phantom.injectJs('lib/utils.js');
```

##处理器

###onError
PhantomJS 1.5开始支持

这个回调函数会在JavaScript执行报错但没有被`page.onError`捕获的时候执行。这是PhantomJS中最接近全局错误捕获的方法，所以最好是设置一个`onError`处理器用来捕获一些没有预期的错误。传递给函数的参数包括错误信息和数组形式的堆栈跟踪。

```
phantom.onError = function(msg, trace) {
    var msgStack = ['PHANTOM ERROR: ' + msg];
    if (trace && trace.length) {
        msgStack.push('TRACE:');
        trace.forEach(function(t) {
            msgStack.push(' -> ' + (t.file || t.sourceURL) + ': ' + t.line + (t.function ? ' (in function ' + t.function +')' : ''));
        });
    }
    console.error(msgStack.join('\n'));
    phantom.exit(1);
};
```
