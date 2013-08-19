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
`href`属性申明这个超链接指向的目的地。如果没有申明href属性，那么这个元素将表现为[placeholder hyperlink](http://www.w3.org/TR/html-markup/a.html#placeholder-hyperlink)。`href`属性可以指向一个URL，也可以指向一个URL片段。URL片段是一个以#符号开始的名字，它在当前文档中申明了一个内部的目标地址（一个`ID`）。URL不是只能指向基于HTTP协议的文档，URL也可以用在任何浏览器支持的协议上。如：`file`、`ftp`和`mailto`等。  
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
该属性申明了这个文档和超链接目的文档之间的关系。属性值为空格分隔的关系列表。The values and their semantics will be registered by some authority that might have meaning to the document author. 当不指定任何关系时，默认值为`void`。  

__注意：当`href`属性申明时再使用本属性__

* hreflang
该属性指定超链接目标使用的语言。HTML4支持的合法的语言标签列表请见[RFC 1766]()，HTML5支持的合法的语言标签列表请见[BCP 47](http://www.w3.org/TR/html-markup/references.html#refsBCP47)。  

__注意：当`href`属性申明时再使用本属性__

* media [HTML5]

The media for which the destination of the hyperlink was designed.
A valid media query list as defined in [Media Queries].


This attribute specifies the media which the linked resource applies to. Its value must be a media query. This attribute is mainly useful when linking to external stylesheets by allowing the user agent to pick the best adapted one for the device it runs on.
Usage note:

In HTML 4, only simple white-space-separated list of media description literals, i.e. media types and groups, where defined and allowed as values for this attribute, like print, screen, aural, braille, ... HTML 5 extended this to any kind of media queries, which are a superset of the allowed values of HTML 4.
Browsers not supporting the CSS3 Media Queries won't necessarilly recognize the adequate link; do not forget to set fallback links, the restricted set of media queries defined in HTML 4.

* type
超链接目标的[MIME](http://www.w3.org/TR/html-markup/datatypes.html#common.data.mimetype)类型。合法的MIME类型列表请见[RFC 2046](http://www.w3.org/TR/html-markup/references.html#refsRFC2046)。  

__注意：当`href`属性申明时再使用本属性__

* download [HTML5]
This attribute, if present, indicates that the author intends the hyperlink to be used for downloading a resource so that when the user clicks on the link they will be prompted to save it as a local file. If the attribute has a value, the value will be used as the pre-filled file name in the Save prompt that opens when the user clicks on the link (the user can change the name before actually saving the file of course). There are no restrictions on allowed values, but you should consider that most file systems have limitations with regard to what punctuation is supported in file names, and browsers are likely to adjust file names accordingly.

Note:
Can be used with blob: URLs and data: URLs, to make it easy for users to download content that is generated programmatically using JavaScript (e.g. a picture created using an online drawing Web app).
If the HTTP header Content-Disposition: is present and gives a different filename than this attribute, the HTTP header has priority over this attribute.
If this attribute is present and Content-Disposition: is set to inline, Firefox gives priority to Content-Disposition, like for the filename case, while Chrome gives priority to the download attribute.
In Firefox 20 this attribute is only honored for links to resources with the same-origin.

* ping [HTML5]
* charset [HTML5中废弃]
This attribute defines the character encoding of the linked resource. The value is a space- and/or comma-delimited list of character sets as defined in RFC 2045. The default value is ISO-8859-1.
Usage note: This attribute is obsolete in HTML5 and should not be used by authors. To achieve its effect, use the HTTP Content-Type header on the linked resource.
* coords [HTML5中废弃]
For use with object shapes, this attribute uses a comma-separated list of numbers to define the coordinates of the object on the page.
* name [HTML5中废弃]
This attribute is required in an anchor defining a target location within a page. A value for name is similar to a value for the id core attribute and should be an alphanumeric identifier unique to the document. Under the HTML 4.01 specification, id and name both can be used with the <a> element as long as they have identical values.
Usage note: This attribute is obsolete in HTML5, use global attribute id instead.
* rev [HTML5中废弃]
This attribute specifies a reverse link, the inverse relationship of the rel attribute. It is useful for indicating where an object came from, such as the author of a document.
* shape [HTML5中废弃]
This attribute is used to define a selectable region for hypertext source links associated with a figure to create an image map. The values for the attribute are circle, default, polygon, and rect. The format of the coords attribute depends on the value of shape. For circle, the value is x,y,r where x and y are the pixel coordinates for the center of the circle and r is the radius value in pixels. For rect, the coords attribute should be x,y,w,h. The x,y values define the upper-left-hand corner of the rectangle, while w and h define the width and height respectively. A value of polygon for shape requires x1,y1,x2,y2,... values for coords. Each of the x,y pairs defines a point in the polygon, with successive points being joined by straight lines and the last point joined to the first. The value default for shape requires that the entire enclosed area, typically an image, be used.
Note: It is advisable to use the usemap attribute for the <img> element and the associated <map> element to define hotspots instead of the shape attribute.
* datafld [非标准]
* datasrc [非标准]
* methods [非标准]
* urn [非标准]
 
##额外的约束和警告
* `a`元素不能是`a`元素的后代。
* `a`元素不能是`button`元素的后代。
* `coords`属性已经在HTML5中废除，对于图片地图，请使用`area`元素代替`a`元素。
* `shape`属性已经在HTML5中废除，对于图片地图，请使用`area`元素代替`a`元素。
* `urn`属性已经在HTML5中废除，Specify the preferred persistent identifier using the href attribute instead.
* `charset`属性已经在HTML5中废除，请使用HTTP`Content-Type`头来代替。
* `methods`属性已经在HTML5中废除，请使用HTTP `OPTIONS`特性来代替。
* `rev`属性已经在HTML5中废除，Use the rel attribute instead, with a term having the opposite meaning.
* `name`属性已经在HTML5中废除，Consider putting an id attribute on the nearest container instead.

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
It is often the case that an anchor tag is used with the onclick event. In order to prevent the page from refreshing, href is often set to either "#" or "javascript:void(0)". Both of these values can lead to some unexpected errors when copying links and opening links in a new tab and/or window. Be aware of this for usability reasons, and when users do use anchor tags and you prevent default behavior.
