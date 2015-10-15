> 贡献者： PoppinLp
> 翻译时间：2015年10月16日
> 原文来源：http://phantomjs.org/api/system/
> 原文作者：PhantomJS
> 原文标题：System Module

# 系统模块

想使用系统模块，必须先将 `system` 模块 `require` 进来：

```js
var system = require('system');
```

- property
    - [args](#args)
    - [env](#env)
    - [os](#os)
    - [pid](#pid)
    - [platform](#platform)

## args

`system.args` {String[]}

查询并返回命令行参数列表。列表中第一项总是脚本名称，之后的是其他后续参数。

下面这个例子输出出所有命令行参数：

```js
var system = require('system');
var args = system.args;

if (args.length === 1) {
    console.log('Try to pass some arguments when invoking this script!');
} else {
    args.forEach(function(arg, i) {
        console.log(i + ': ' + arg);
    });
}
```

## env

`system.env` {Object}

查询并返回表示环境变量的键值对列表。

下面这个例子和 Unix 中 `printenv` 命令或者 Windows 中 `set` 命令功能类似：

```js
var system = require('system');
var env = system.env;

Object.keys(env).forEach(function(key) {
    console.log(key + '=' + env[key]);
});
```

## os

`system.os` {Object}

只读。表示一个提供了操作系统信息的对象，包括系统架构、名称、版本等。例如：

```js
var system = require('system');
var os = system.os;
console.log(os.architecture);  // '32bit'
console.log(os.name);  // 'windows'
console.log(os.version);  // '7'
```

## pid

`system.pid` {Number}

引入版本：PhantomJS 1.8

只读。表示当前执行 PhantomJS 进程的 PID（Process ID）。

## platform

`system.platform` {String}

只读。表示当前平台的名字，该值总是为 `'phantomjs'`。

例子：

```js
var system = require('system');
console.log(system.platform); // 'phantomjs'
```
