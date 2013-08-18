> 贡献者：梁鹏  
> 翻译时间：2013年8月16日  
> 原文来源：http://www.nodejs.org/api/net.html  
> 原文作者：NodeJS  
> 原文标题：Net  

#网络
> Stability: 3 - Stable
`net`模块提供了和网络相关的异步操作封装。它同时包括了创建服务端和客户端的方法。你可以通过`require('net')`来引入这个模块。

##net.createServer([options], [connectionListener])
该方法用于创建一个TCP连接的服务端。

`connectionListener`参数会被自动设置为[connection事件](#connection-event)的监听器。

`options`参数是一个对象，它的默认状态如下：
```
{
    allowHalfOpen: false
}
```
当`allowHalfOpen`参数被设置为`true`时，这个socket在收到另一端的FIN包后将不会自动回复FIN包。这个socket将会成为可写但不可读的。你应该明确的调用`end()`方法。更多内容请看[end事件](#end-event)。

这是一个监听8124端口上的连接的服务器端的例子：
```
var net = require('net');
var server = net.createServer(function(c) { //'connection' listener
    console.log('server connected');
    c.on('end', function() {
        console.log('server disconnected');
    });
    c.write('hello\r\n');
    c.pipe(c);
});
server.listen(8124, function() { //'listening' listener
    console.log('server bound');
});
```
可以通过使用`telnet`来测试它：
```
telnet localhost 8124
```
如果想要监听`/tmp/echo.sock`，那么只需要将倒数第三行改为：
```
server.listen('/tmp/echo.sock', function() { //'listening' listener
```
使用`nc`来连接UNIX domain socket服务器端：
```
nc -U /tmp/echo.sock
```

##net.connect(options, [connectionListener]) 和 net.createConnection(options, [connectionListener])
该方法创建一个新的socket对象，并且连接到给定的地址。当socket建立时，[connect事件](#connect-event)将会被触发。

对于TCP socket，`options`参数应该是一个如下构成的对象：
* `port`（必须）：客户端应该连接的端口号。
* `host`：客户端应该连接的主机。默认是`localhost`。
* `localAddress`：用来绑定网络连接的本地接口。

对于Unix domain socket，`options`参数应该是一个如下构成的对象：
* `path`（必须）：客户端应该连接的地址。

通用的`options`参数有：
* `allowHalfOpen`：当`allowHalfOpen`参数被设置为`true`时，这个socket在收到另一端的FIN包后将不会自动回复FIN包。默认是`false`。更多内容请看[end事件](#end-event)。

`connectListener`参数将会被作为[connect事件](#connect-event)的监听器。

这是一个使用`net.connetct`方法的客户端例子：
```
var net = require('net');
var client = net.connect({port: 8124},
    function() { //'connect' listener
        console.log('client connected');
        client.write('world!\r\n');
    });
client.on('data', function(data) {
    console.log(data.toString());
    client.end();
});
client.on('end', function() {
    console.log('client disconnected');
});
```
如果想连接`/tmp/echo.sock`，那么只需要将第二行改为：
```
var client = net.connect({path: '/tmp/echo.sock'},
```

##net.connect(port, [host], [connectListener]) 和 net.createConnection(port, [host], [connectListener])
对于某个主机的某个端口创建一个TCP连接。`host`参数缺省值为`localhost`。`connectListerner`参数将会被作为[connect事件](#connect-event)的监听器。

##net.connect(path, [connectListener]) 和 net.createConnection(path, [connectListener])
创建一个Unix socket连接到某个地址。`connectListerner`参数将会被作为[connect事件](#connect-event)的监听器。

##Class: net.Server
_这段先略过。_

##Class: net.Socket
这个对象是一个TCP和UNIX socket的抽象。`net.Socket`的实例实现了一个基于流的双工的接口。他们可以被用户创建并作为客户端使用（通过`connect()`），也可以被NODE创建并通过服务器端的[connection事件](#connection-event)传递给用户。

###new net.Socket([options])
创建一个新的socket对象。

`options`参数是一个拥有以下默认值的对象：
```
{
    fd: null
    type: null
    allowHalfOpen: false
}
```
`fd`参数允许你指定已经存在的socket文件描述符。  
`type`参数指定相关的协议。可以是`tcp4`、`tcp6`或者`unix`。
关于`allowHalfOpen`参数，请看`createServer()`和[end事件](#end-event)。

###socket.connect(port, [host], [connectListener]) 和 socket.connect(path, [connectListener])
Opens the connection for a given socket. If port and host are given, then the socket will be opened as a TCP socket, if host is omitted, localhost will be assumed. If a path is given, the socket will be opened as a unix socket to that path.

Normally this method is not needed, as net.createConnection opens the socket. Use this only if you are implementing a custom Socket.

This function is asynchronous. When the 'connect' event is emitted the socket is established. If there is a problem connecting, the 'connect' event will not be emitted, the 'error' event will be emitted with the exception.

The connectListener parameter will be added as an listener for the 'connect' event.

socket.bufferSize#
net.Socket has the property that socket.write() always works. This is to help users get up and running quickly. The computer cannot always keep up with the amount of data that is written to a socket - the network connection simply might be too slow. Node will internally queue up the data written to a socket and send it out over the wire when it is possible. (Internally it is polling on the socket's file descriptor for being writable).

The consequence of this internal buffering is that memory may grow. This property shows the number of characters currently buffered to be written. (Number of characters is approximately equal to the number of bytes to be written, but the buffer may contain strings, and the strings are lazily encoded, so the exact number of bytes is not known.)

Users who experience large or growing bufferSize should attempt to "throttle" the data flows in their program with pause() and resume().

###socket.setEncoding([encoding])
该方法设置当socket作为输入流时的编码。更多详情，请查看`stream.setEncoding()`。

###socket.write(data, [encoding], [callback])
Sends data on the socket. The second parameter specifies the encoding in the case of a string--it defaults to UTF8 encoding.

Returns true if the entire data was flushed successfully to the kernel buffer. Returns false if all or part of the data was queued in user memory. 'drain' will be emitted when the buffer is again free.

The optional callback parameter will be executed when the data is finally written out - this may not be immediately.

###socket.end([data], [encoding])
Half-closes the socket. i.e., it sends a FIN packet. It is possible the server will still send some data.

If data is specified, it is equivalent to calling socket.write(data, encoding) followed by socket.end().

###socket.destroy()
Ensures that no more I/O activity happens on this socket. Only necessary in case of errors (parse error or so).

###socket.pause()
该方法暂停读取数据。也就是说，data事件不会被触发。主要用来throttle back an upload.

###socket.resume()
该方法恢复由于执行`pause()`导致的暂停。

###socket.setTimeout(timeout, [callback])
Sets the socket to timeout after timeout milliseconds of inactivity on the socket. By default net.Socket do not have a timeout.

When an idle timeout is triggered the socket will receive a 'timeout' event but the connection will not be severed. The user must manually end() or destroy() the socket.

If timeout is 0, then the existing idle timeout is disabled.

The optional callback parameter will be added as a one time listener for the 'timeout' event.

###socket.setNoDelay([noDelay])
Disables the Nagle algorithm. By default TCP connections use the Nagle algorithm, they buffer data before sending it off. Setting true for noDelay will immediately fire off data each time socket.write() is called. noDelay defaults to true.

###socket.setKeepAlive([enable], [initialDelay])
Enable/disable keep-alive functionality, and optionally set the initial delay before the first keepalive probe is sent on an idle socket. enable defaults to false.

Set initialDelay (in milliseconds) to set the delay between the last data packet received and the first keepalive probe. Setting 0 for initialDelay will leave the value unchanged from the default (or previous) setting. Defaults to 0.

###socket.address()
该方法返回socket绑定的地址，其中地址的协议和端口号是由操作系统提供的。返回的对象有3个属性，如：{ port: 12346, family: 'IPv4', address: '127.0.0.1' }

###socket.unref()
在一个socket上调用`unref`方法将会允许程序在该socket是事件系统中唯一活动的socket时自动退出。如果一个socket已经执行了`unref`方法，那么再次执行`unref`方法是无效的。

###socket.ref()
与`unref`相反，在一个执行过`unref`方法的socket上执行`ref`方法，将不会允许程序在该socket是事件系统中唯一活动的socket时自动退出（这也是默认的做法）。如果一个socket已经执行了`ref`方法，那么再次执行`ref`方法是无效的。

###socket.remoteAddress
远程IP地址。如：`74.125.127.100`或者`2001:4860:a005::68`。

###socket.remotePort
远程端口号。如：`80`或者`21`。

###socket.localAddress
远程服务器端连接的本地IP地址。如：当你在监听`0.0.0.0`时，远程客户端连接`192.168.1.1`，那么这个值为`192.168.1.1`。

###socket.localPort
本地端口号。如：`80`或者`21`。

###socket.bytesRead
已接收的字节数。

###socket.bytesWritten
已发送的字节数。

###Event: 'connect'
该事件在一个socket连接成功构建时触发。可以看看`connect()`方法。

###Event: 'data'
`Buffer object`
该事件在获取到数据时触发。`data`参数是一个`Buffer`或者`String`。数据的编码通过`socket.setEncoding()`方法来设置。（更多详情，请查看[Readable Stream]()章节。）

Note that the data will be lost if there is no listener when a Socket emits a 'data' event.

###Event: 'end'
当另一端的socket发送FIN包时发生。  
By default (allowHalfOpen == false) the socket will destroy its file descriptor once it has written out its pending write queue. However, by setting allowHalfOpen == true the socket will not automatically end() its side allowing the user to write arbitrary amounts of data, with the caveat that the user is required to end() their side now.

###Event: 'timeout'
Emitted if the socket times out from inactivity. This is only to notify that the socket has been idle. The user must manually close the connection.
参考资料：`socket.setTimeout()`

###Event: 'drain'
该事件当写缓存为空时发生。能被用来做throttle uploads(断点续传？)。  
参考资料：`socket.wirte()`方法的返回值

###Event: 'error'
* `Error object`
当有错误发生时该事件被触发。close事件将在该事件之后被触发。

###Event: 'close'
* had_error `Boolean` 当socket有传输错误时，值为`true`
该事件在socket完全结束时发生。`had_error`参数是个用来标识socket是否是因为传输错误而结束的布尔值。

##net.isIP(input)
该方法用来检查`input`是否是一个IP地址。如果是非法字符串，返回0；如果是IPv4地址，返回4；如果是IPv6地址，返回6。

##net.isIPv4(input)
如果`input`为IPv4的地址，该方法返回`true`，否则返回`false`。

##net.isIPv6(input)
如果`input`为IPv6的地址，该方法返回`true`，否则返回`false`。
