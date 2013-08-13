> 贡献者：梁鹏  
> 翻译时间：2013年8月13日  
> 原文来源：http://www.w3.org/TR/html-markup/label.html  
> 原文作者：W3C  
> 原文标题：head – caption for a form control  

#label
label元素通常是一个表单的控制单元的标题。

##支持的内容
包含[普通文字信息](http://www.w3.org/TR/html-markup/syntax.html#normal-character-data)的[修饰性元素](http://www.w3.org/TR/html-markup/common-models.html#common.elem.phrasing)

##支持的属性
* [global attributes](http://www.w3.org/TR/html-markup/global-attributes.html)  
_global attributes即任何通用的属性、事件和方法。_
* for
_该属性的值为将这个label作为标题的表单元素的id_
* form [new]
_该属性的值为想要被关联到的表单的id_
 
##额外的约束和警告
* label元素不能自身嵌套
* label元素能包含最多一个input、button、select、textarea元素
* label元素的for属性如果存在的话，只能指向表单控制元素
* 

##标签省略
* 当head元素是以某一个元素开头的时候，开标签<head>可以省略。
* 当head元素之后紧跟着的不是空格或者注释的时候，闭标签</head>可以省略。  
_大多数浏览器在head标签有省略的时候，都能自动的对其进行补全，但也有部分老的浏览器不会这么做。 [相关文章](http://www.stevesouders.com/blog/2010/05/12/autohead-my-first-browserscope-user-test/)_

##允许的父元素
html元素  
_head元素常常作为html元素的第一个子元素。_

##DOM接口
```
interface HTMLHeadElement : HTMLElement {};
```

##默认的display属性
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
