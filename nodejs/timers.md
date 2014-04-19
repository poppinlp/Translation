> 贡献者：梁鹏  
> 翻译时间：2014年4月19日  
> 原文来源：http://www.nodejs.org/api/timers.html  
> 原文作者：NodeJS  
> 原文标题：Timers  

#Timers
> Stability: 5 - Locked

所有的计时器方法都是全局的，不需要通过`require()`这个模块来使用这些方法。

##setTimeout(callback, delay, [arg], [...])
安排一个一次性的`callback`函数在`delay`毫秒的延迟时间后执行。返回一个给`clearTimeout()`提供的`timeoutObject`。通过可选参数你可以给回调函数传递参数。

需要说明一下的是你的回调函数可能不是那么精确的刚好在`delay`毫秒后执行，也就是说Node.js不保证回调函数精确的执行时间，也不保证会按照顺序执行。回调函数将会尽可能的在靠近延迟的时间被调用。

##clearTimeout(timeoutObject)
阻止一个`timeoutObject`。

##setInterval(callback, delay, [arg], [...])
安排一个循环执行的`callback`函数在每隔`delay`毫秒的延迟时间后执行。返回一个给`clearInterval()`提供的`intervalObject`。通过可选参数你可以给回调函数传递参数。

##clearInterval(intervalObject)
停止一个`intervalObject`。

##unref()
通过`setTimeout`和`setInterval`返回的计时器特殊值包含一个`timer.unref()`方法，该方法允许你创建一个激活的计时器但如果这是事件循环中唯一的一项那么程序将不会运行。如果一个计时器已经执行了`unref`方法，那么再次调用`unref`方法是无效的。

在通过`setTimeout`调用`unref`时，其实就是创建了一个单独的将会唤醒事件循环的计时器。创建太多这样的内容将会对事件循环的性能造成一定的影响，所以需要合理的使用。

##ref()
如果你之前对一个计时器调用了`unref()`方法，那么可以通过`ref()`方法来显示的请求计时器保持程序打开。如果一个计时器已经调用了`ref`方法，再次调用`ref`方法是无效的。

##setImmediate(callback, [arg], [...])
在I/O事件回调执行后并且在`setTimerout`和`setInterval`之前安排`callback`回调函数的执行。返回一个给`clearImmediate()`提供的`immediateObject`。通过可选参数你可以给回调函数传递参数。

这类即时函数被放在创建的队列中，在每个循环迭代中被队列被逐一取出执行。这和`process.nextTick`不同的是`process.nextTick`在每次循环迭代的时候执行数量会有`process.maxTickDepth`的限制。在队列中的回调执行后，如果I/O处于停止状态，`setImmediate`将会屈服于事件循环。虽然执行的顺序是保证的，但是其他I/O可以在任何两个安排好的即时函数间执行。

##clearImmediate(immediateObject)
停止一个`immediateObject`。
