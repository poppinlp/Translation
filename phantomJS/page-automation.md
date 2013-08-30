> 贡献者：梁鹏  
> 翻译时间：2013年8月30日  
> 原文来源：https://github.com/ariya/phantomjs/wiki/Page-Automation    
> 原文作者：PhantomJS  
> 原文标题：Page Automation  

#网页自动化

因为PhantomJS能加载并操作网页，所以用它来做网页自动化方面的事情将是非常棒的。

##操作DOM

因为脚本就像再浏览器中一样被执行，所以标准的[DOM操作](http://en.wikipedia.org/wiki/DOM_scripting)和[CSS选择器](http://www.w3.org/TR/css3-selectors/)多能正常被使用。

下面这个`useragent.js`例子演示了如何从id为`myagent`的节点上获取`textContent`属性：

```
var page = require('webpage').create();
console.log('The default user agent is ' + page.settings.userAgent);
page.settings.userAgent = 'SpecialAgent';
page.open('http://www.httpuseragent.org', function (status) {
    if (status !== 'success') {
        console.log('Unable to access network');
    } else {
        var ua = page.evaluate(function () {
            return document.getElementById('myagent').textContent;
        });
        console.log(ua);
    }
    phantom.exit();
});
```

上面这个例子同样也演示了如何自定义远程web服务器获取到的UA。

##使用jQuery和其他库

在1.6版本中，你能使用通过page.includeJs来在页面中引入jQuery，例如：

```
var page = require('webpage').create();
page.open('http://www.sample.com', function() {
    page.includeJs("http://ajax.googleapis.com/ajax/libs/jquery/1.6.1/jquery.min.js", function() {
        page.evaluate(function() {
            $("button").click();
        });
        phantom.exit()
    });
});
```

上面这个例子将会打开一个网页，引入jQeury，并且通过jQuery来点击所有的按钮。然后会关闭该网页。注意应该在引入jQuery之后的执行代码中关闭网页，否则网页可能在引入的JS代码执行之前就关闭了。
