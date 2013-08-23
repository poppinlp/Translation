> 贡献者：梁鹏  
> 翻译时间：2013年8月13日  
> 原文来源：http://www.w3.org/TR/html-markup/a.html  
> 原文作者：W3C  
> 原文标题：a - hyperlink  

#a
a元素表现为一个超链接。

##支持的内容
任何[行内元素](http://www.w3.org/TR/html-markup/common-models.html#common.elem.phrasing)和[块级元素](http://www.w3.org/TR/html-markup/common-models.html#common.elem.flow)。  

##支持的属性
* [global attributes](http://www.w3.org/TR/html-markup/global-attributes.html)  
任何通用的属性、事件和方法。

* href
`href`属性申明这个超链接指向的目的地。如果没有申明href属性，那么这个元素将表现为[placeholder hyperlink](http://www.w3.org/TR/html-markup/a.html#placeholder-hyperlink)。`href`属性可以指向一个URL，也可以指向一个锚。锚是一个以`#`符号开始的名字，它在当前文档中申明了一个内部的目标地址（一个`ID`）。URL不是只能指向基于HTTP协议的文档，URL也可以用在任何浏览器支持的协议上。如：`file`、`ftp`和`mailto`等。  
__注意：你可以使用`top`这个特殊的片段名来创建一个回到页面顶部的链接，例如`<a href="#top">Return to top</a>`。这是HTML5中申明的用法。__

* target
这个属性申明显示链接资源的地方。在HTML4中，它是个frame的名字或者关键字；在HTML5中，它是个浏览器上下文的名字或者关键字（例如tab、window或者内联frame）。下面是有特殊含义的关键字列表：（每个表现情况均分为HTML4和HTML5两种）
    * _self  
    在相同的frame或者浏览器上下文中读取响应。这是`target`属性的默认值。
    * _blank  
    在新的窗口或者浏览器上下文中读取响应。
    * _parent  
    在当前frame的父级frame或者当前浏览器上下文的父级浏览器上下文中读取响应。如果没有父级环境，这个选项和`_self`的表现相同。
    * _top  
    在取消掉其他所有frame的原始窗口或者最顶级的浏览器上下文中读取响应。如果没有父级环境，这个选项和`_self`的表现相同。

__注意：当`href`属性申明时再使用本属性__

* rel
该属性申明了这个文档和超链接目的文档之间的关系。属性值为空格分隔的关系列表。那些对于作者可能有一定意义的属性值和他们的语意将会被某些权威识别。当不指定任何关系时，默认值为`void`。  
__注意：当`href`属性申明时再使用本属性__

* hreflang
该属性指定超链接目标使用的语言。HTML4支持的合法的语言标签列表请见[RFC 1766](http://www.ietf.org/rfc/rfc1766.txt)，HTML5支持的合法的语言标签列表请见[BCP 47](http://www.w3.org/TR/html-markup/references.html#refsBCP47)。  
__注意：当`href`属性申明时再使用本属性__

* media [HTML5]
该属性定义了超链接目标的多媒体类型。它的值必须是一个`media query`。这个属性主要是针对那些允许用户UA自适应用户设备的页面。一个有效的`media query`列表定义在[Media Queries](http://www.w3.org/TR/html-markup/references.html#refsMediaQueries)。

* type
超链接目标的[MIME](http://www.w3.org/TR/html-markup/datatypes.html#common.data.mimetype)类型。合法的MIME类型列表请见[RFC 2046](http://www.w3.org/TR/html-markup/references.html#refsRFC2046)。  
__注意：当`href`属性申明时再使用本属性__

* download [HTML5]
就像他的名字一样，这个属性就是用来指定用下载的方式链接到资源，把资源保存到本地文件。如果该属性有值，这个值会被用作下载时的默认文件名。对于属性值没有严格的限制，但使用的时候应该考虑大多数操作系统对于文件名的限制。

注意：
    * 可以被用来指定blob和data，让用户更容易的下载javascript程序生成的内容（比如在线画图工具生成的图片）。
    * 当HTTP返回头中包含`Content-Disposition`并且提供了另一个文件名，那么讲采用返回头中的文件名而不是这个属性的文件名。
    * 当HTTP返回头中包含`Content-Disposition`并且其值为inline，Firefox给`Content-Disposition`更高的优先级，Chrome给`download`属性更高的优先级。
    * 在Firefox 20中，这个属性仅仅对同源的资源有效。

* ping [HTML5]
由空格分隔的URL列表，当用户点击该链接时，这些URL会获得通知。  
__注意：当`href`属性申明时再使用本属性__
* charset [HTML5中废弃]
* coords [HTML5中废弃]
* name [HTML5中废弃]
* rev [HTML5中废弃]
* shape [HTML5中废弃]
* datafld [非标准]
* datasrc [非标准]
* methods [非标准]
* urn [非标准]
 
##额外的约束和警告
* `a`元素不能是`a`元素的后代。
* `a`元素不能是`button`元素的后代。
* `coords`属性已经在HTML5中废除，对于图片地图，请使用`area`元素代替`a`元素。
* `shape`属性已经在HTML5中废除，对于图片地图，请使用`area`元素代替`a`元素。
* `urn`属性已经在HTML5中废除，指定首选的持久标识符请使用`href`属性代替。
* `charset`属性已经在HTML5中废除，请使用HTTP`Content-Type`头来代替。
* `methods`属性已经在HTML5中废除，请使用HTTP`OPTIONS`特性来代替。
* `rev`属性已经在HTML5中废除，请使用带有相反意思的`rel`属性代替。
* `name`属性已经在HTML5中废除，考虑通过在最近的父元素上设置`id`属性来代替。

##标签省略
a元素必须同时包含开标签和闭标签，不能省略。

##允许的父元素
任何能包含[行内元素](http://www.w3.org/TR/html-markup/common-models.html#common.elem.phrasing)以及[块级元素](http://www.w3.org/TR/html-markup/common-models.html#common.elem.flow)的元素

##HTML5中的改变
尽管之前版本的HTML严格要求`a`元素只能包含行内元素，但现在没有这个限制了。也就是说，当某个`a`元素的实例它的父元素允许包含块级元素时，这个`a`元素是可以包含块级元素的。

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
<a href="http://www.meituan.com/">美团网</a>
```

##关于javascript:void(0)
大多数时候`a`元素的使用都伴随着鼠标点击事件的触发。为了阻止页面的刷新，`href`属性经常被设置为`#`或者`javascript:void(0)`。`#`即一个页面上端的锚，而`void`是javascript中的一个操作符，作用就是计算一个表达式，但不返回值，如`void(document.form.submit())`就会提交表单，而`void(0)`则没有任何效果。
