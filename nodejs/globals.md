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

A reference to the current module. In particular `module.exports` is used for defining what a module exports and makes available through require().

module isn't actually a global but rather local to each module.

See the [module system documentation](http://nodejs.org/api/modules.html) for more information.

##exports
A reference to the `module.exports` that is shorter to type. See [module system documentation](http://nodejs.org/api/modules.html) for details on when to use exports and when to use `module.exports`.

`exports` isn't actually a global but rather local to each module.

See the [module system documentation](http://nodejs.org/api/modules.html) for more information.

See the [module section](http://nodejs.org/api/modules.html) for more information.

##setTimeout(cb, ms)
启动一个计时器，在`ms`毫秒后执行回调函数`cb`。实际上延迟的时间取决于一些外部因素如系统计时器的粒度和系统负载。

延迟的时间值必须在1-2147483647之间。如果延迟的时间超过这个范围，那么将会被设置成1毫秒。广义上讲，一个计时器的有效期不能超过24.8天。

返回一个代表着计时器的值。

##clearTimeout(t)
停止一个之前通过`setTimeout()`创建的计时器。那个计时器的回调函数不会被执行。

##setInterval(cb, ms)
启动一个计时器，每隔`ms`毫秒就执行一次回调函数`cb`。注意实际上的延迟不一定准确，取决于一些外部因素如系统计时器的粒度和系统负载。但
Run callback `cb` repeatedly every `ms` milliseconds. Note that the actual interval may vary, depending on external factors like OS timer granularity and system load. It's never less than ms but it may be longer.

The interval must be in the range of 1-2,147,483,647 inclusive. If the value is outside that range, it's changed to 1 millisecond. Broadly speaking, a timer cannot span more than 24.8 days.

Returns an opaque value that represents the timer.

##clearInterval(t)
Stop a timer that was previously created with `setInterval()`. The callback will not execute.

The timer functions are global variables. See the [timers](http://nodejs.org/api/timers.html) section.
