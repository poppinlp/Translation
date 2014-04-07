> 贡献者：梁鹏  
> 翻译时间：2014年4月7日  
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
Use the internal `require()` machinery to look up the location of a module, but rather than loading the module, just return the resolved filename.

##require.cache
{Object}

Modules are cached in this object when they are required. By deleting a key value from this object, the next `require` will reload the module.

##__filename
{String}

The filename of the code being executed. This is the resolved absolute path of this code file. For a main program this is not necessarily the same filename used in the command line. The value inside a module is the path to that module file.

Example: running `node example.js` from `/Users/mjr`

```
console.log(__filename);
// /Users/mjr/example.js
```

`__filename` isn't actually a global but rather local to each module.

##__dirname
{String}

The name of the directory that the currently executing script resides in.

Example: running `node example.js` from `/Users/mjr`

```
console.log(__dirname);
// /Users/mjr
```

`__dirname` isn't actually a global but rather local to each module.

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
Run callback `cb` after at least `ms` milliseconds. The actual delay depends on external factors like OS timer granularity and system load.

The timeout must be in the range of 1-2,147,483,647 inclusive. If the value is outside that range, it's changed to 1 millisecond. Broadly speaking, a timer cannot span more than 24.8 days.

Returns an opaque value that represents the timer.

##clearTimeout(t)
Stop a timer that was previously created with `setTimeout()`. The callback will not execute.

##setInterval(cb, ms)
Run callback `cb` repeatedly every `ms` milliseconds. Note that the actual interval may vary, depending on external factors like OS timer granularity and system load. It's never less than ms but it may be longer.

The interval must be in the range of 1-2,147,483,647 inclusive. If the value is outside that range, it's changed to 1 millisecond. Broadly speaking, a timer cannot span more than 24.8 days.

Returns an opaque value that represents the timer.

##clearInterval(t)
Stop a timer that was previously created with `setInterval()`. The callback will not execute.

The timer functions are global variables. See the [timers](http://nodejs.org/api/timers.html) section.
