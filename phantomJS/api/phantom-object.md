> 贡献者： PoppinLp  
> 翻译时间：2015年10月11日  
> 原文来源：http://phantomjs.org/api/phantom/  
> 原文作者：PhantomJS  
> 原文标题：Phantom Object  

# Phantom Object

The interface with various PhantomJS functionalities is carried out using a new host object named phantom, added as a child of the window object.

- property
    - [args](#args)
    - [cookies](#cookies)
    - [cookiesEnabled](#cookiesEnabled)
    - [libraryPath](#libraryPath)
    - [scriptName](#scriptName)
    - [version](#version)
- method
    - [addCookie](#addCookie)
    - [deleteCookie](#deleteCookie)
    - [clearCookies](#clearCookies)
    - [exit](#exit)
    - [injectJs](#injectJs)
- event
    - [onError](#onError)

## args

`phantom.args` {String[]}

稳定性：不推荐使用 - 请使用 System 模块的 `system.args`

只读。表示传递给这个脚本的参数数组。

## cookies

`phantom.cookies` {Object[]}

引入版本：PhantomJS 1.7

获取或设置任何一个域名的 Cookie（不过更推荐通过 `phantom.addCookie` 来设置 Cookie）。这些 Cookie 将先储存在 CookieJar 中，然后一起在打开相关页面的时候应用。

如果在 PhantomJS 的启动配置里提供了 Cookie 文件，那么里面的数据将会被预先填进这个数组里。

## cookiesEnabled

`phantom.cookiesEnabled` {Boolean}

引入版本：PhantomJS 1.7

控制是否启用 CookieJar。默认为 `true`。

## libraryPath

`phantom.libraryPath` {String}

这个属性保存着用来给 `injectJs` 函数确定脚本目录的路径。这个值最初是 PhantomJS 执行的脚本所在的路径。

## scriptName

`phantom.scriptName` {String}

稳定性：不推荐使用 - 请使用 System 模块的 `system.args[0]`

只读。表示执行的脚本文件的名字。

## version

`phantom.version` {Object}

只读。表示执行的 PhantomJS 的版本。例如：`{ 'major': 1, 'minor': 7, 'patch': 0 }`。

## addCookie

`phantom.addCookie(Object)` {Boolean}

引入版本：PhantomJS 1.7

添加一个 Cookie 到 CookieJar。
添加成功返回 `true`，否则返回 `false`。

例子：

```js
phantom.addCookie({
    'name': 'Added-Cookie-Name',
    'value': 'Added-Cookie-Value',
    'domain': '.google.com'
});
```

## clearCookies

`phantom.clearCookies()` {void}

引入版本：PhantomJS 1.7

删除 CookieJar 中的所有 Cookie。

## deleteCookie

`phantom.deleteCookie(cookieName)` {Boolean}

引入版本：PhantomJS 1.7

删除 CookieJar 中某个特定名字的 Cookier。
删除成功返回 `true`，否则返回 `false`。

例子：

```js
phantom.deleteCookie('Added-Cookie-Name');
```

## exit

`phantom.exit(returnValue)` {void}

以给定的返回值结束程序。如果没设置返回值，默认为 `0`。

例子：

```js
if (somethingIsWrong) {
    phantom.exit(1);
} else {
    phantom.exit(0);
}
```

## injectJs

`phantom.injectJs(filename)` {boolean}

从指定的文件注入外部脚本代码到 Phantom。如果当前目录中不存在该文件，将会在 `libraryPath` 路径中查找。
注入成功返回 `true`，否则返回 `false`。

例子：

```js
var wasSuccessful = phantom.injectJs('lib/utils.js');
```

## onError

引入版本：PhantomJS 1.7

这个事件当产生了没有被 `page.onError` 处理的 JavaScript 运行时错误时触发。
因为这是 PhantomJS 中最接近于全局错误处理的方式，所以通常建议绑定上这个 `onError` 事件以防止产生未被捕获的程序异常。
回掉函数的参数是错误信息和相关的调用堆栈（数组）。

例子：

```js
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
