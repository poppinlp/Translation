> 贡献者：梁鹏  
> 翻译时间：2013年8月13日  
> 原文来源：http://www.w3.org/TR/html-markup/head.html  
> 原文作者：W3C  
> 原文标题：head - document metadata container  

#head
`head`元素是一个文档`metadata`的集合，包括内联和外联的脚本和样式表。

##支持的内容
* title  
除非文档是以`iframe`形式被嵌入的，或者`title`以其它的形式提供了，否则`title`元素都是应该添加的。
* base
* basefont
* bgsound
* link
* meta
* nextID
* script
* style

##支持的属性
* [global attributes](http://www.w3.org/TR/html-markup/global-attributes.html)  
任何全局的属性。
 
##额外的约束和警告
`head`元素包含一个`profile`属性，该属性是一个由空格分隔的 URL 列表，这些 URL 包含着有关页面的元数据信息。  
`profile`属性在HTML4中支持，但是在HTML5中被废弃了。所以当需要注册[meta extensions](http://wiki.whatwg.org/wiki/MetaExtensions)的时候，请直接申明在文档中需要用到的`meta`元素；当需要针对UA触发特定的行为的时候，用一个`link`元素代替。

##标签省略
* 当`head`元素是以某一个元素开头的时候，开标签`<head>`可以省略。
* 当`head`元素之后紧跟着的不是空格或者注释的时候，闭标签`</head>`可以省略。  
_注意：大多数浏览器在`head`标签有省略的时候，都能自动的对其进行补全，但也有部分老的浏览器不会这么做。 [相关文章](http://www.stevesouders.com/blog/2010/05/12/autohead-my-first-browserscope-user-test/)_

##允许的父元素
html元素  
`head`元素常常作为`html`元素的第一个子元素。

##DOM接口
```
interface HTMLHeadElement : HTMLElement {};
```

##典型的默认显示属性
```
head {
    display:none;
}
```

##浏览器支持情况
所有浏览器都支持。

##例子
```
<html>
    <head>
        <title>example</title>
    </head>
</html>
```
