> 贡献者：梁鹏  
> 翻译时间：2013年8月13日  
> 原文来源：http://www.w3.org/TR/html-markup/label.html  
> 原文作者：W3C  
> 原文标题：label - caption for a form control  

#label
label元素表现为一个表单的控制单元的标题。

##支持的内容
包含[普通字符](http://www.w3.org/TR/html-markup/syntax.html#normal-character-data)的[修饰性元素](http://www.w3.org/TR/html-markup/common-models.html#common.elem.phrasing)

##支持的属性
* [global attributes](http://www.w3.org/TR/html-markup/global-attributes.html)  
任何通用的属性、事件和方法。
* for
该属性的值为希望被这个label绑定的元素的id。
* form [HTML5]
该属性的值为想要被关联到的表单的id。
* accesskey [HTML4 HTML5]
该属性用来设置这个label对应的键盘快捷键。如当accesskey值为1时，键盘按下alt+1即可为label绑定的元素设置焦点。  
_注意：当鼠标点击label时，在触发label的onclick事件后会触发label绑定元素的onclick事件；但通过accesskey设置的快捷键则只会设置焦点，不会触发onclick事件。_
 
##额外的约束和警告
* label元素不能自身嵌套。
* label元素能包含最多一个input、button、select或textarea元素。
* label元素的for属性如果存在的话，只能指向表单的控制单元。
* label元素不能作为a元素的子元素。
* label元素不能作为button元素的子元素。

##标签省略
label元素必须同时包含开标签和闭标签，不能省略。

##允许的父元素
任何能包含[修饰性元素](http://www.w3.org/TR/html-markup/common-models.html#common.elem.phrasing)的元素

##DOM接口
```
interface HTMLLabelElement : HTMLElement {
    readonly    attribute HTMLFormElement? form;
                attribute DOMString htmlFor;
    readonly    attribute HTMLElement? control;
};
```

##典型的默认显示属性
```
label {
    cursor:default;
}
```

##浏览器支持情况
所有浏览器都支持。

##例子
* label元素的隐式使用

```
<label>Click me<input type="text" id="Name" name="Name" /></label>
```
* label元素的显式使用

```
<label for="Name">Click me</label>
<input type="text" id="Name" name="Name" />
```
