> 贡献者： PoppinLp
> 翻译时间：2015年10月11日
> 原文来源：http://phantomjs.org/api/child_process/
> 原文作者：PhantomJS
> 原文标题：Child Process Module

# 子进程模块

`child_process` 模块允许你创建子进程并通过 stdin / stdout / stderr 与他们通信。
当需要执行打印、发送邮件、执行其他语言的脚本或程序的时候，这将十分有用。

想使用子进程模块，必须先将 `child_process` 模块 `require` 进来：

```js
var process = require("child_process")
var spawn = process.spawn
var execFile = process.execFile

var child = spawn("ls", ["-lF", "/rooot"])

child.stdout.on("data", function (data) {
    console.log("spawnSTDOUT:", JSON.stringify(data))
})

child.stderr.on("data", function (data) {
    console.log("spawnSTDERR:", JSON.stringify(data))
})

child.on("exit", function (code) {
    console.log("spawnEXIT:", code)
})

//child.kill("SIGKILL")

execFile("ls", ["-lF", "/usr"], null, function (err, stdout, stderr) {
    console.log("execFileSTDOUT:", JSON.stringify(stdout))
    console.log("execFileSTDERR:", JSON.stringify(stderr))
})
```

## spawn

例子：

```js
var page  = require('page').create();
var spawn = require('child_process').spawn;

page.open('http://google.com', function(status){
  if( status == 'success' ) {
    page.render('/tmp/google-snapshot.jpg');
    spawn('/usr/bin/sensible-browser', 'file:///tmp/google-snapshot.jpg');
    phantom.exit();
  }
})
```
