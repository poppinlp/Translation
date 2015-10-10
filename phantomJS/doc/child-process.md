> 贡献者：PoppinLp  
> 翻译时间：2014年4月20日  
> 原文来源：https://http://phantomjs.org/api/child_process/  
> 原文作者：PhantomJS  
> 原文标题：Child Process Module  

#Child Process Module
该模块允许你开启子进程并且通过stdin/stdout/stderr来和它们通信。对于像打印、发送邮件或者调用其他语言写的脚本和程序这类型的任务，这个模块非常有用。

该模块需要先`require`才能使用。

```
var childProcess = require('child_process');
```

##方法

###spawn
