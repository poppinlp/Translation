> 贡献者：梁鹏  
> 翻译时间：2014年4月19日  
> 原文来源：http://www.nodejs.org/api/querystring.html  
> 原文作者：NodeJS  
> 原文标题：Query String  

#Query String
> Stability: 3 - Stable

这个模块提供了一些处理查询参数的常用方法。

##querystring.stringify(obj, [sep], [eq])
把一个对象序列化为字符串。其中分隔符和赋值符是可选的，默认为`&`和`=`。

例子：

```
querystring.stringify({ foo: 'bar', baz: ['qux', 'quux'], corge: '' })
// returns
'foo=bar&baz=qux&baz=quux&corge='

querystring.stringify({foo: 'bar', baz: 'qux'}, ';', ':')
// returns
'foo:bar;baz:qux'
```

##querystring.parse(str, [sep], [eq], [options])
把字符串反序列化为一个对象。其中分隔符和赋值符死可选的，默认为`&`和`=`。

最后一个可选的对象可以包含`maxKeys`属性（默认为1000），该属性是用来限制健值对的最大数量的。可以设置为0来取消最大数量的限制。

例子：

```
querystring.parse('foo=bar&baz=qux&baz=quux&corge')
// returns
{ foo: 'bar', baz: ['qux', 'quux'], corge: '' }
```

##querystring.escape
这是`querystring.stringify`使用的函数编码函数，如果需要的话可以自定义。

##querystring.unescape
这是`querystring.parse`使用的函数解码函数，如果需要的话可以自定义。
