> 贡献者：梁鹏  
> 翻译时间：2013年8月13日  
> 原文来源：http://expressjs.com/guide.html  
> 原文作者：express团队  
> 原文标题：express-guide  

#express-guide

##开始

在安装了node的情况下，通过在你的电脑中任意一个位置创建一个目录来开始我们的express之旅。如  
```
$ mkdir hello-world
```

现在，你就可以开始开发属于自己的node包啦。首先，你需要根据express的要求创建一个package.json文件。你可以使用npm info express version来查看最新的express版本。为了防止以后的兼容性问题，我们推荐你不要使用3.x以下的版本。下面是一个package.json的例子。  
```
{
    "name": "hello-world",
    "description": "hello world test app",
    "version": "0.0.1",
    "private": true,
    "dependencies": {
        "express": "3.x"
    }
}
```

在拥有了一个package.json文件后，你便可以使用下面的方法来自动安装依赖的node包，在这个例子中只有express：  
```
$ npm install
```

在npm安装结束后，你便能在当前目录下发现一个叫做node_modules的目录，里面便是刚才安装的node包。你可以通过npm ls命令来查看node包之间的依赖关系，会显示如下的树状图  
```
$ npm ls
hello-world@0.0.1 /private/tmp
└─┬ express@3.0.0beta7
  ├── commander@0.6.1
  ├─┬ connect@2.3.9
  │ ├── bytes@0.1.0
  │ ├── cookie@0.0.4
  │ ├── crc@0.2.0
  │ ├── formidable@1.0.11
  │ └── qs@0.4.2
  ├── cookie@0.0.3
  ├── debug@0.7.0
  ├── fresh@0.1.0
  ├── methods@0.0.1
  ├── mkdirp@0.3.3
  ├── range-parser@0.0.4
  ├─┬ response-send@0.0.1
  │ └── crc@0.2.0
  └─┬ send@0.0.3
    └── mime@1.2.6
```

现在我们来创建应用本身吧。首先根据你的喜好创建一个叫做app.js或者server.js的文件，然后通过express()来创建一个应用：  
```
var express = require('express');
var app = express();
```

在应用中你可以通过app.VERB()来设置路由。如在下面这个例子中"get /"会回应"Hello World"字符串，其中req和res都是node提供给你的对象，所以你可以调用res.pipe(),req.on('data', callback)或者其他的任何与express无关的方法。  
```
app.get('/hello.txt', function(req, res) {
    var body = 'Hello World';
    res.setHeader('Content-Type', 'text/plain');
    res.setHeader('Content-Length', body.length);
    res.end(body);
});
```

但express给这些参数赋予了更高级的方法。比如res.send()，这个方法除了其他的功能还会自动的为你添加Content-Length：  
```
app.get('/hello.txt', function(req, res) {
    res.send('Hello World');
});
```

现在我们通过调用app.listen()方法来监听用户的链接吧，这个方法和node的net.Server#listen()方法接受同样的参数：  
```
app.listen(3000);
console.log('Listening on port 3000');
```

##使用express来开发一个应用

express绑定了一个友好的可执行的工具express()。如果你是通过下面这种全局的方式来安装express的，你便可以在机器的任何地方使用它：  
```
$ npm install -g express
```

这个工具提供了一种很简单的方式来创建应用的框架，但同样也有些限制。比如它只支持一部分模板引擎，而express则支持所有node上的模板引擎。详情可以通过--help来确认：  
```
Usage: express [options]
Options:
-h, --help          output usage information
-V, --version       output the version number
-s, --sessions      add session support
-e, --ejs           add ejs engine support (defaults to jade)
-J, --jshtml        add jshtml engine support (defaults to jade)
-H, --hogan         add hogan.js engine support
-c, --css   add stylesheet  support (less|stylus) (defaults to plain css)
-f, --force         force on non-empty directory
```

如果你想使用EJS来开发一个支持session功能的应用，你只需要执行：  
```
$ express --sessions --css stylus --ejs myapp
create : myapp
create : myapp/package.json
create : myapp/app.js
create : myapp/public
create : myapp/public/javascripts
create : myapp/public/images
create : myapp/public/stylesheets
create : myapp/public/stylesheets/style.styl
create : myapp/routes
create : myapp/routes/index.js
create : myapp/views
create : myapp/views/index.ejs
install dependencies:
$ cd myapp && npm install
run the app:
$ node app 
```
	
像其他node应用一样，你必须安装它的依赖node包：  
```
$ cd myapp
$ npm install
```

然后，对你的应用说"走你"：  
```
$ node app
```

这就是运行一个简单的应用你需要做的所有事情。请记住express没有绑定到任何特定的目录结构，这些都只是你工作的开始。想获取更多应用框架，请去[_这个网址_](https://github.com/visionmedia/express/tree/master/examples)寻找。

##错误处理

"错误处理"的中间件在定义上和普通的中间件并无区别，不过它必须包含4个参数(err, req, res, next)：  
```
app.use(function(err, req, res, next) {
    console.error(err.stack);
    res.send(500, 'Something broke!');
});
```

虽说不是强制的，但"错误处理"中间件通常被定义在相对与其他app.use()靠后的地方：  
```
app.use(express.bodyParser());
app.use(express.methodOverride());
app.use(app.router);
app.use(function(err, req, res, next) {
    // logic
});
```

中间件给出的响应格式可以是很随意的，比如你可以返回一个html错误页面，一个简单的错误信息，一段json数据或者是任何你希望的东西。  
出于结构化和高级框架的考虑，你可能需要像其他中间件那样，定义多个"错误处理"的中间件。例如如果你想定义一个针对XHR的"错误处理"中间件以及其他的，你可以这么做：  
```
app.use(express.bodyParser());
app.use(express.methodOverride());
app.use(app.router);
app.use(logErrors);
app.use(clientErrorHandler);
app.use(errorHandler);
```

这里的通用logErrors可能会把错误信息输出到stderr，日志或者类似的服务：  
```
function logErrors(err, req, res, next) {
    console.error(err.stack);
    next(err);
}
```

这里的clientErrorHandler是如下定义的，注意错误是明确的传递给了下一个  
```
function clientErrorHandler(err, req, res, next) {
    if (req.xhr) {
        res.send(500, { error: 'Something blew up!' });
    } else {
        next(err);
    }
}
```

这里的errorHandler负责捕获所有的的错误，可以这样定义它：  
```
function errorHandler(err, req, res, next) {
    res.status(500);
    res.render('error', { error: err });
}
```

##在线用户统计

这一部分将介绍一个完整的使用Redis(http://redis.io/)来统计用户在线数量的应用。首先，你需要创建一个包含两个依赖关系的package.json文件(例如下面这个)，其中一个依赖关系是redis，另一个就是express。并且你也需要安装redis，然后通过$ redis-server 来运行它。  
```
{
    "name": "app",
    "version": "0.0.1",
    "dependencies": {
        "express": "3.x",
        "redis": "*"
    }
}
```

然后，你需要创建一个应用，然后把它链接到redis：  
```
var express = require('express');
var redis = require('redis');
var db = redis.createClient();
var app = express();
```

接着是用来跟踪在线用户的一个中间件。这里我们使用有序集合，以便于我们向redis查询在过去的N毫秒里在线的用户。我们通过传递一个时间戳来作为每个用户的标记。注意这里我们使用了User-Agent字符串替代了通常使用的用户id。  
```
app.use(function(req, res, next) {
    var ua = req.headers['user-agent'];
    db.zadd('online', Date.now(), ua, next);
});
```

我们还需要一个获得最近一分钟里在线用户的中间件。如下面的代码，通过使用zrevrangebyscore并伴随着一个正无穷大的值，我们便能获取到1分钟内的最近用户。  
```
app.use(function(req, res, next) {
    var min = 60 * 1000;
    var ago = Date.now() - min;
    db.zrevrangebyscore('online', '+inf', ago, function(err, users) {
        if (err) return next(err);
        req.online = users;
        next();
    });
});
```

最后，让我们来把它绑定到某个端口上，然后使用它吧！这样我们就完工啦，通过多个浏览器来访问这个应用，然后你就能看到在线用户数量的增加。  
```
app.get('/', function(req, res) {
    res.send(req.online.length + ' users online');
});
app.listen(3000);
```

##使用代理

在例如Varnish或者Nginx这类的反向代理下使用express是不常见的，虽然它并不需要什么配置。可以直接通过app.enable('trust proxy')来激活"trust proxy"设置，在激活后express就能知道它是在代理之下工作的，并且平时不可信的头部标签 X-Forwarded-* 也是可信的。  
激活了这个设置后会产生一些微妙的影响。首先就是 X-Forwarded-Proto 可能是反向代理设置的用来告诉应用当前是http还是https链接，这个值是req.protocol的映射。其次这会使得espress用 X-Forwarded-For 的地址列表来填充req.ip和req.ips。
