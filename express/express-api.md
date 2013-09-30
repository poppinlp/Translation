> 贡献者：梁鹏  
> 翻译时间：2013年9月30日  
> 原文来源：http://expressjs.com/api.html  
> 原文作者：express团队  
> 原文标题：express-api  

#express-api

##Application

###express()

创建一个express应用。

```
var express = require('express');
var app = express9);

app.get('/', function (req, res) {
    res.send('hello world');
});

app.lisiten(3000);
```

###app.set(name, value)

设置`name`为`value`。

```
app.set('title', 'My Site');
app.get('title');
// => "My Site"
```

###app.get(name)

获取`name` 的值。

```
app.get('title');
// => undefined

app.set('title', 'My Site');
app.get('title');
// => "My Site"
```

###app.enable(name)

设置`name`为`true`。

```
app.enable('trust proxy');
app.get('trust proxy');
// => true
```

###app.disable(name)

设置`name`为`false`。

```
app.disable('trust proxy');
app.get('trust proxy');
// => false
```

###app.enabled(name)

检查`name`是否启用

```
app.enabled('trust proxy');
// => false

app.enable('trust proxy');
app.enabled('trust proxy');
// => true
```

###app.disabled(name)

检查`name`是否未启用

```
app.disabled('trust proxy');
// => true

app.enable('trust proxy');
app.disabled('trust proxy');
// => false
```

###app.configure([env], callback)

当`env`匹配`app.get('env')`(即`process.env.NODE_ENV`)时调用`callback`。保留这个方法是因为历史原因，下面给出的`if`实现性能表现会更好。该方法__不是__必须的，可以使用`app.set()`和其他设置函数代替。

```
// all environments
app.configure(function(){
    app.set('title', 'My Application');
})

// development only
app.configure('development', function(){
    app.set('db uri', 'localhost/dev');
})

// production only
app.configure('production', function(){
    app.set('db uri', 'n.n.n.n/prod');
})
```

更好的实现：

```
// all environments
app.set('title', 'My Application');

// development only
if ('development' == app.get('env')) {
    app.set('db uri', 'localhost/dev');
}

// production only
if ('production' == app.get('env')) {
    app.set('db uri', 'n.n.n.n/prod');
}
```

###app.use([path], function)

使用提供的中间件`function`。加载`path`为可选设置，默认是"/"。

```
var express = require('express');
var app = express();

// simple logger
app.use(function(req, res, next){
    console.log('%s %s', req.method, req.url);
    next();
});

// respond
app.use(function(req, res, next){
    res.send('Hello World');
});

app.listen(3000);
```
