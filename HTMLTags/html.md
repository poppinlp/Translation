> 贡献者：梁鹏  
> 翻译时间：2014年4月19日  
> 原文来源：http://www.w3.org/TR/html-markup/html.html  
> 原文作者：W3C  
> 原文标题：html - root element  

#html
`html`元素是一个文档的根节点，所有其他的元素都是它的子孙。

##支持的内容
一个`head`元素，后面跟着一个`body`元素。

##支持的属性
* [global attributes](http://www.w3.org/TR/html-markup/global-attributes.html)  
任何全局的属性。
* manifest [HTML5]  
当前文档缓存配置文件的地址（用来控制离线是缓存内容的）。
* version [HTML5中废弃]
 
##额外的约束和警告
* `html`元素的`version`属性已经过时了，可以安全的省略它。

##标签省略
如果`html`元素中第一个内容不是注释，那么`html`元素的开始标签可以省略。

如果`html`元素后面不是紧跟着注释并且内部的`body`元素非空且`body`元素的开始标签没省略，那么`html`元素的结束标签可以省略。

##允许的父元素
这是文档的根元素。

##HTML5中的改变
尽管之前版本的HTML严格要求`a`元素只能包含行内元素，但现在没有这个限制了。也就是说，当某个`a`元素的实例它的父元素允许包含块级元素时，这个`a`元素是可以包含块级元素的。

##DOM接口
```
interface HTMLHtmlElement : HTMLElement {};
```

##典型的默认显示属性
```
html {
    display: block;
}
html:focus {
    outline: none;
}
```

##浏览器支持情况
* 基本的支持
    * 所有浏览器都支持。
