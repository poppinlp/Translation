> 贡献者：PoppinLp  
> 翻译时间：2014年4月20日  
> 原文来源：https://phantomjs.org/api/system/  
> 原文作者：PhantomJS  
> 原文标题：System Module  

#System Module
该模块需要先`require`才能使用。

```
var system = require('system');
```

##属性

###args
`system.args` {String[]}

查询并返回命令行参数的列表，其中第一个是脚本名称，之后跟随着其他的参数。

下面的例子输出了所有命令行参数：

```
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

###env
`system.env` {Object}

查询并返回环境变量的健值对列表。

下面的例子和Unix的`printenv`工具以及Windows的`set`命令有相同的作用：

```
var system = require('system');
var env = system.env;

Object.keys(env).forEach(function(key) {
    console.log(key + '=' + env[key]);
});
```

###os

该属性只读，是一个提供了操作系统信息的对象，包括`architectur`、`name`和`version`。

例子：

```
var system = require('system');
var os = system.os;
console.log(os.architecture);  // '64bit'
console.log(os.name);  // 'mac'
console.log(os.version);  // 'unknow'
```

###pid
`system.pid` {Number}

PhantomJS 1.8开始支持。该属性只读，是当前PhantomJS进程的PID（Process ID）。

###platform
`system.platform` {String}

该属性只读，是当前平台的名字，也就是`'phantomjs'`。

例子：

```
var system = require('system');
console.log(system.platform); // 'phantomjs'
```
