> 贡献者：梁鹏  
> 翻译时间：2013年8月16日  
> 原文来源：http://www.nodejs.org/api/synopsis.html  
> 原文作者：NodeJS  
> 原文标题：Synopsis  

#概述
这是一个简单的用NODE写的返回Hello World的网络服务的例子：  
```
var http = require('http');

http.createServer(function (request, response) {
    response.writeHead(200, {'Content-Type': 'text/plain'});
    response.end('Hello World\n');
}).listen(8124);

console.log('Server running at http://127.0.0.1:8124/');
```

为了执行这个服务，把代码放进一个叫"example.js"的文件中，然后通过NODE程序来执行它：  
```
> node example.js
Server running at http://127.0.0.1:8124/
```

这一系列文档中所有的例子都能通过类似的方式来执行。
