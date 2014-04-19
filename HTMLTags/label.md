> 贡献者：梁鹏  
> 翻译时间：2013年8月13日  
> 原文来源：http://www.w3.org/TR/html-markup/label.html  
> 原文作者：W3C  
> 原文标题：label - caption for a form control  

#label
`label`元素表现为一个表单的控制单元的标题。

##支持的内容
包含[普通字符](http://www.w3.org/TR/html-markup/syntax.html#normal-character-data)的[行内元素](http://www.w3.org/TR/html-markup/common-models.html#common.elem.phrasing)

##支持的属性
* [global attributes](http://www.w3.org/TR/html-markup/global-attributes.html)  
任何全局的属性。
* for  
该属性的值为希望被这个`label`绑定的元素的id。
* accesskey [HTML4 HTML5]  
该属性用来设置这个`label`对应的键盘快捷键。如当`accesskey`值为1时，键盘按下alt+1即可为`label`绑定的元素设置焦点。请不要将快捷键设置为如下的通常被浏览器使用的值：a、c、e、f、g、h、v。  
_注意：当鼠标点击`label`时，在触发`label`的`onclick`事件后会触发`label`绑定元素的`onclick`事件；但通过`accesskey`设置的快捷键则只会设置焦点，不会触发`onclick`事件。_
* form [HTML5]  
该属性的值为想要被关联到的表单的`id`。
 
##额外的约束和警告
* `label`元素不能自身嵌套。
* `label`元素能包含最多一个`input`、`button`、`select`或`textarea`元素。
* `label`元素的`for`属性如果存在的话，只能指向表单的控制单元。
* `label`元素不能作为`a`元素的子元素。
* `label`元素不能作为`button`元素的子元素。

##标签省略
`label`元素必须同时包含开标签和闭标签，不能省略。

##允许的父元素
任何能包含[行内元素](http://www.w3.org/TR/html-markup/common-models.html#common.elem.phrasing)的元素

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
