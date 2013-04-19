一.Application

    1.express()
        创建一个express应用。如：
        var express = require('express');
        var app = express();
        app.get('/', function(req, res) {
            res.send('hello world');
        });
        app.listen(3000);

    2.app.set(name, value)
        为应用增加一个value值的name属性。如：
        app.set('title', 'my site');
        app.get('title');
        //  =>  'my site'
        
    3.app.get(name)
        获取应用的name属性。如：
        app.set('title', 'my site');
        app.get('title');
        // => 'my site'

    4.app.enable(name)
        使name属性可用(为true)。如：
        app.enable('trust proxy');
        app.get('trust proxy');
        // => true

    5.app.disable(name)
        使name属性不可用(为false)。如：
        app.disable('trust proxy');
        app.get('trust proxy');
        // => false
        
    6.app.enabled(name)
        检查属性name是否是可用的。如：
        app.enabled('trust proxy');
        // => false
        app.enable('trust proxy');
        app.enabled('trust proxy');
        // => true

    7.app.disabled(name)
        检查属性name是否是不可用的。如：
        app.disabled('trust proxy');
        // => true
        app.enable('trust proxy');
        app.disabled('trust proxy');
        // => false

    8.app.configure([env], callback)
        当参数env的值等于app.get('env')，也就是process.env.NODE_ENV时，调用函数callback。

    9.app.use()
    10.app.engine()
    11.app.param()
    12.application settings
    13.application routing
    14.app.all()
    15.app.locals
    16.app.render()
    17.app.routes
    18.app.listen()

二.Request

    1.req.params
        这个属性是一个包含了所有映射到以命名的路由'parameters'的属性的数组。比如如果你有一个路由叫做/user/:name，那么你可以通过req.params.name来访问这里面的name。这个对象默认是{}。
    2.req.query
    3.req.body
    4.req.files
    5.req.param()
    6.req.route
    7.req.cookies
    8.req.signedCookies
    9.req.get()
    10.req.accepts()
    11.req.accepted
    12.req.is()
    13.req.ip
    14.req.ips
    15.req.path
    16.req.host
    17.req.fresh
    18.req.stale
    19.req.xhr
    20.req.protocol
    21.req.secure
    22.req.subdomains
    23.req.originalUrl
    24.req.acceptedLanguages
    25.req.acceptedCharsets
    26.req.acceptsCharset()
    27.req.acceptsLanguage()

三.Response
四.Middleware
