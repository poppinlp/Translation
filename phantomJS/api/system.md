> 贡献者： PoppinLp
> 翻译时间：2015年10月11日
> 原文来源：http://phantomjs.org/api/child_process/
> 原文作者：PhantomJS
> 原文标题：Child Process Module

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

Queries and returns a list of the command-line arguments. The first one is always the script name, which is then followed by the subsequent arguments.

例子：

```js
The following example prints all of the command-line arguments:

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

system.env {Object}

Queries and returns a list of key-value pairs representing the environment variables.

例子：

The following example demonstrates the same functionality as the Unix printenv utility or the Windows set command:

```js
var system = require('system');
var env = system.env;

Object.keys(env).forEach(function(key) {
    console.log(key + '=' + env[key]);
});
```

## os

Read-only. An object providing information about the operating system, including architecture, name, and version. For example:

例子：

```js
var system = require('system');
var os = system.os;
console.log(os.architecture);  // '32bit'
console.log(os.name);  // 'windows'
console.log(os.version);  // '7'
```

## pid

system.pid {Number}

Introduced: PhantomJS 1.8 Read-only. The PID (Process ID) for the currently executing PhantomJS process.

例子：

```js
var system = require('system');
// @TODO: Finish system.pid example.
```

## platform

system.platform {String}

Read-only. The name of the platform, for which the value is always 'phantomjs'.

例子：

```js
var system = require('system');
console.log(system.platform); // 'phantomjs'
```
