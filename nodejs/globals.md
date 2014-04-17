> 贡献者：梁鹏  
> 翻译时间：2014年4月13日  
> 原文来源：http://www.nodejs.org/api/globals.html  
> 原文作者：NodeJS  
> 原文标题：Global Objects  

#全局对象
这些对象在所有模块中都可以使用。其中有些是在模块作用域中但不在全局作用域中，这会被标注出来。

##global
{Object} 全局命名空间对象。

在浏览器中，最顶层的作用域就是全局作用域。这就是说在浏览器中，如果你在全局作用域里`var something`将会申明一个全局变量。但在Node环境中不尽相同。最顶层的作用域不是全局作用域，在一个Node模块内部`var something`将只能在那个模块中访问。

##process
{Object}

进程对象，详情可以看[process object](http://nodejs.org/api/process.html#process_process)。

##console
{Object}

用来输出内容到标准输出流和标准错误流。详情可以看[console](http://nodejs.org/api/console.html)。

##Class: Buffer
{Function}

用来处理二进制数据。详情可以看[buffer](http://nodejs.org/api/buffer.html)。

##require()
{Function}

用来引用模块。详情可以看[Modules](http://nodejs.org/api/modules.html#modules_modules)。`require`其实不是一个全局变量，而是存在于每个模块中。

##require.resolve()
使用内置的`require()`机制去定位模块的位置，但并不加载模块，只是返回解析后的文件名。

##require.cache
{Object}

当模块被加载后它们就缓存在这个对象中。在删除对象中的某个键值后，下一次`require`会重新加载这个对象。

##__filename
{String}

即当前执行代码的文件名。这是代码文件解析后的绝对路径。对于主程序而言这和命令行中的文件名不一定相同。对于一个模块而言这是模块文件的路径。

例如：在`/Users/mjr/`中执行`node example.js`

```
console.log(__filename);
// /Users/mjr/example.js
```

`__filename`其实不是全局变量，但在每个模块中都可以访问。

##__dirname
{String}

当前执行的脚本所在的目录名。

例如：在`Users/mjr`中执行`node example.js`

```
console.log(__dirname);
// /Users/mjr
```

`__dirname`其实不是全局变量，但在每个模块中都可以访问。

##module
{Object}

是当前模块的引用。`module.exports`用来定义一个模块通过`require()`来引用的对外接口。

`module`其实不是全局变量，但在每个模块中都可以访问。

可以查看[module system documentation](http://nodejs.org/api/modules.html)文档来获取更多信息。

##exports
是`module.exports`的引用的简写形式。在使用`exports`或`module.exports`时可以查看[module system documentation](http://nodejs.org/api/modules.html)获取详情。

`exports`其实不是全局变量，但在每个模块中都可以访问。

可以查看[module system documentation](http://nodejs.org/api/modules.html)和[module section](http://nodejs.org/api/modules.html)文档来获取更多信息。

##setTimeout(cb, ms)
启动一个计时器，在`ms`毫秒后执行回调函数`cb`。实际上延迟的时间取决于一些外部因素如系统计时器的粒度和系统负载。

延迟的时间值必须在1-2147483647之间。如果延迟的时间超过这个范围，那么将会被设置成1毫秒。广义上讲，一个计时器的有效期不能超过24.8天。

返回一个代表着计时器的特殊值。

##clearTimeout(t)
停止一个之前通过`setTimeout()`创建的计时器。那个计时器的回调函数不会被执行。

##setInterval(cb, ms)
启动一个计时器，每隔`ms`毫秒就执行一次回调函数`cb`。注意实际上的延迟不一定准确，取决于一些外部因素如系统计时器的粒度和系统负载。但只会更长不会更短。

延迟的时间值必须在1-2147483647之间。如果延迟的时间超过这个范围，那么将会被设置成1毫秒。广义上讲，一个计时器的有效期不能超过24.8天。

返回一个代表着计时器的特殊值。

##clearInterval(t)
停止一个之前通过`setInterval()`创建的计时器。那个计时器的回调函数不会被执行。

计时器函数时全局表量。详情可以看[这篇文档](http://nodejs.org/api/timers.html).
