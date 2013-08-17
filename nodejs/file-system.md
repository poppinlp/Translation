> 贡献者：梁鹏  
> 翻译时间：2013年8月16日  
> 原文来源：http://www.nodejs.org/api/fs.html  
> 原文作者：NodeJS  
> 原文标题：File System  

#文件系统
> Stability: 3 - Stable

文件的读写是基于对标准POSIX函数简单的封装来实现的。执行require('fs')就能使用这个模块。所有方法都有异步和同步两个版本。  
异步版本通常最后一个参数都是一个回调函数。回调函数的参数根据不同的方法会有所差异，不过第一个参数通常都用来处理异常。如果这个是成功的，那么第一个参数将会是null或者undefined。  
当使用同步版本时，所有的异常都是立刻被抛出的。你可以使用try/catch语句来处理异常，或者让它们继续抛出。  

这是一个使用异步版本的例子：  
```
var fs = require('fs');

fs.unlink('/tmp/hello', function (err) {
    if (err) throw err;
    console.log('successfully deleted /tmp/hello');
});
```

这是一个使用同步版本的例子：  
```
var fs = require('fs');

fs.unlinkSync('/tmp/hello')
console.log('successfully deleted /tmp/hello');
```

异步执行的方法没有明确的顺序，所以下面的代码可能有错：  
```
fs.rename('/tmp/hello', '/tmp/world', function (err) {
    if (err) throw err;
    console.log('renamed complete');
});
fs.stat('/tmp/world', function (err, stats) {
    if (err) throw err;
    console.log('stats: ' + JSON.stringify(stats));
});
```

fs.stat可能在fs.rename之前执行。所以正确的做法应该是把回调函数组成一个链：  
```
fs.rename('/tmp/hello', '/tmp/world', function (err) {
    if (err) throw err;
    fs.stat('/tmp/world', function (err, stats) {
        if (err) throw err;
        console.log('stats: ' + JSON.stringify(stats));
    });
});
```

在实际使用中，强烈建议开发者使用这些方法的异步版本。因为同步版本在执行结束之前，会一直阻塞整个进程。  
可以使用相对路径来定位，然后请记住，相对路径是相对于process.cwd()来定位的。  
大多数fs中的方法允许你省略回调函数，如果你这么做的话，一个默认的回调函数将会被执行。它会忽略错误，并输出一个deprecation warning。  
__注意: Omitting the callback is deprecated. v0.12 will throw the errors as exceptions.__

##fs.rename(oldPath, newPath, callback)
rename方法的异步版本。回调函数的参数只有一个，即可能存在的异常。

##fs.renameSync(oldPath, newPath)
rename方法的同步版本。

##fs.ftruncate(fd, len, callback)
ftruncate方法的异步版本。回调函数的参数只有一个，即可能存在的异常。

##fs.ftruncateSync(fd, len)
ftruncate方法的同步版本。

##fs.truncate(path, len, callback)
truncate方法的异步版本。回调函数的参数只有一个，即可能存在的异常。

##fs.truncateSync(path, len)
truncate方法的同步版本。

##fs.chown(path, uid, gid, callback)
chown方法的异步版本。回调函数的参数只有一个，即可能存在的异常。

##fs.chownSync(path, uid, gid)
chown方法的同步版本。

##fs.fchown(fd, uid, gid, callback)
fchown方法的异步版本。回调函数的参数只有一个，即可能存在的异常。

##fs.fchownSync(fd, uid, gid)
fchown函数的同步版本。

##fs.lchown(path, uid, gid, callback)
lchown方法的异步版本。回调函数的参数只有一个，即可能存在的异常。

##fs.lchownSync(path, uid, gid)
lchown函数的同步版本。

##fs.chmod(path, mode, callback)
chmod方法的异步版本。回调函数的参数只有一个，即可能存在的异常。

##fs.chmodSync(path, mode)
chmod方法的同步版本。
