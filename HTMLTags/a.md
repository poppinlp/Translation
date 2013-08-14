> 贡献者：梁鹏  
> 翻译时间：2013年8月13日  
> 原文来源：http://www.w3.org/TR/html-markup/a.html  
> 原文作者：W3C  
> 原文标题：a - hyperlink  

#a
a元素表现为一个超链接。

##支持的内容

##支持的属性
* [global attributes](http://www.w3.org/TR/html-markup/global-attributes.html)  
任何通用的属性、事件和方法。
* href
* target
* rel
* hreflang
* media
* type
超链接目标的[MIME type](http://www.w3.org/TR/html-markup/datatypes.html#common.data.mimetype)
 
##额外的约束和警告

##标签省略
a元素必须同时包含开标签和闭标签，不能省略。

##允许的父元素
任何能包含[修饰性元素](http://www.w3.org/TR/html-markup/common-models.html#common.elem.phrasing)以及[流元素](http://www.w3.org/TR/html-markup/common-models.html#common.elem.flow)的元素

##DOM接口
```
interface HTMLAnchorElement : HTMLElement {
    stringifier attribute DOMString href;
    attribute DOMString target;

    attribute DOMString rel;
    readonly attribute DOMTokenList relList;
    attribute DOMString media;
    attribute DOMString hreflang;
    attribute DOMString type;

    attribute DOMString text;

    // URL decomposition IDL attributes
    attribute DOMString protocol;
    attribute DOMString host;
    attribute DOMString hostname;
    attribute DOMString port;
    attribute DOMString pathname;
    attribute DOMString search;
    attribute DOMString hash;
};
```

##典型的默认显示属性
```
a:link, a:visited {
    color: (internal value);
    text-decoration: underline;
    cursor: auto;
}
a:link:active, a:visited:active {
    color: (internal value);
}
```

##浏览器支持情况
* 基本的支持
    * 所有浏览器都支持。
* href="#top"的支持
    * Firefox 10.0+
    * 其他浏览器都支持
* download属性
    * Chrome 14+
    * Firefox 20.0+
    * IE 不支持
    * Opera 不支持

##例子
```
```
