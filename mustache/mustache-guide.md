> 贡献者：梁鹏  
> 翻译时间：2013年5月26日  
> 原文来源：http://mustache.github.io/mustache.5.html  
> 原文作者：Chris Wanstrath  
> 原文标题：MUSTACHE MANUAL  

#mustache官方手册

##名称
mustache 一种逻辑化的less模板  

##简介
下面是一个典型的mustache模板  
```
Hello {{name}}
You have just won ${{value}}!
{{#in_ca}}
    Well, ${{taxed_value}}, after taxes.
{{/in_ca}}
```

给它提供下面的哈希表  
```
{
    "name": "Chris",
    "value": 10000,
    "taxed_value": 10000 - (10000 * 0.4),
    "in_ca": true
}
```

将会生成如下的结果  
```
Hello Chris
You have just won $10000!
Well, $6000.0, after taxes.
```

##描述
mushtache能被用在html，设置文件，源代码等各种地方。它通过使用提供的哈希表或者对象来替换模板中的标记。  
我们称它为“逻辑化的less”是因为它不提供if和else的判断以及for循环，提供的只有标记。其中一些标记用来替换哈系值，而另一些标记则用来做其他事情。这个文档将mustache中对各种不同的标记进行详细的介绍。  

##标记类型
所有标记都被两个花括号包裹，如{{person}}是一个标记，{{#person}}也是，不过在这两个例子中我们更推荐用person来做标记。下面让我们来讲讲不同类型标记的区别。  

###1. 变量  
变量是最基本的标记。在模板中遇到{{name}}时，mustache将会尝试着去提供的数据中寻找name值，如果找不到则什么的不会被显示。  
默认所有变量都是经过html编码的，如果你想获得未经html编码的值，请使用三个花括号，如{{{name}}}。  
你也可以使用&符号去获得未经html编码的值，如{{& name}}。特别是当你需要变更分隔符的时候，这将会很好用(有关变更分隔符，请看下面关于“设置分隔符”的部分)。  
默认情况下，如果找不到变量，将会返回空的字符串，不过你可以在mustache的库里进行设置，例如ruby版本的mustache就支持在这种情况下提供例外。下面是关于变量的一个例子。  
模板：  
```
{{name}}
{{age}}
{{company}}
{{{company}}}
```

哈系表：  
```
{
    "name": "chris",
    "company": "<b>GitHub</b>"
}
```
    
输出：  
```
Chris
&lt;b&gt;GitHub&lt;/b&gt;
<b>GitHub</b>
```

###2. 段落  
段落根据其对应的哈希值在当前的上下文中输出一次或者多次的整块文本。  
一个段落通过#开始，并以/结束。如{{#person}}开始一个person段落，{{/person}}则结束它。  
段落的具体行为由其对应的哈希值来决定。  

* False值或者空列表

如果这个person对应的哈系值存在，并且是false值或者是空列表，那么在段落中的html同样不会被显示，下面是一个例子。  
模板： 
```
Shown.
{{#nothin}}
    Never shown!
{{/nothin}}
```

哈系表：  
```
{
    "person": true,
}
```
    
输出：
```
Shown.
```

* 非空列表

如果这个person对应的哈希值存在并且是非空列表，那么在段落中的html将会被显示一次或者多次。  
当这个列表非空时，对于列表中的每一项，段落中的文字都会显示一次。在每次迭代中，段落里的标签都会设置为当前的列表项。通过这种方式，我们可以对一个集合进行循环操作，下面是一个例子。  
模板：  
```
{{#repo}}
    <b>{{name}}</b>
{{/repo}}
```
    
哈希表：  
```
{
    "repo": [
        { "name": "resque" },
        { "name": "hub" },
        { "name": "rip" },
    ]
}
```
    
输出：  
```
<b>resque</b>
<b>hub</b>
<b>rip</b>
```

* 表达式

当值为函数或者表达式等可以被执行的对象时，这个对象将会被传入段落中并进行调用。被传进段落的是没有被处理过的字符串，内部的标签还没有被替换，表达式需要自己来处理。通过这种方式，你可以。下面是一个例子。   
模板：  
```
{{#wrapped}}
    {{name}} is awesome.
{{/wrapped}}
```
    
哈系表：  
```
{
    "name": "Willy",
    "wrapped": function() {
        return function(text) {
            return "<b>" + render(text) + "</b>"
        }
    }
}
```
    
输出：  
```
<b>Willy is awesome.</b>
```

* 非false的值

当值为非false但不是列表时，该值仅仅会被用于替换掉原标签。下面是一个例子。   
模板：  
```
{{#person?}}
    Hi {{name}}!
{{/person?}}
```
    
哈希表：  
```
{
    "person?": { "name": "Jon" }
}
```
    
输出：  
```
Hi Jon!
```

###3. 非段落
一个非段落以^开始并以/结束，例如{{^person}}是person非段落的开始，而{{/person}}是它的结束。  
段落是一次或者多次的基于哈希表来进行文字处理，而非段落可以对非条件进行一次处理。换句话说，非段落会当变量不存在，为false值或者为空列表时进行文字处理。下面是一个例子。  
模板：  
```
{{#repo}}
    <b>{{name}}</b>
{{/repo}}
{{^repo}}
    No repos :(
{{/repo}}
```

哈希表：  
```
{
    "repo": []
}
```

输出：  
```
No repos :(
```

###4. 注释  
注释以！开始，例如下面这个模板  
```
<h1>Today{{! ignore me }}.</h1>
```
    
将会被处理为  
```
<h1>Today.</h1>
```
    
注释可以包含新的行。  

###5. 子模板  
子模板以>开始，例如{{> box}}。  
子模板在运行时被处理，所以可以实现递归行为，但要注意防止无限循环。  
子模板也继承调用环境。在ERB时，你也许会这样做  
```
<%= partial :next_more, :start => start, :size => size %>
```
    
但mustache需要仅仅是  
```
{{> next_more}}
```
    
为什么呢？因为这个next_more.mustache文件将会从调用环境里继承size和start方法。  
看到这里，你也许会想起includes操作或者template扩展。其实他们和子模板的确很像，尽管名字看起来不那么相似。例如  
```
base.mustache:
<h2>Names</h2>
{{#names}}
    {{> user}}
{{/names}}
user.mustache:
<strong>{{name}}</strong>
```

其实处理之后就是这样  
```
<h2>Names</h2>
{{#names}}
    <strong>{{name}}</strong>
{{/names}}
```

###6. 设置分隔符  
设置分隔符的标签以=开始，然后用自定义的字符串替换{{和}}。  
让我们来看一个有些做作的例子  
```
* {{default_tags}}
{{=<% %>=}}
* <% erb_style_tags %>
<%={{ }}=%>
* {{ default_tags_again }}
```
    
这里我们拥有一个包含3个项的列表。第一项使用默认的分隔符，第二项使用了一个通过设置分隔符标签自定义的分隔符，第三项则通过设置分隔符标签设置回了默认的分隔符。  
根据CTemplate的说明，这对于例如TeX之类的文本中会出现{{或者}}并且标记起来不太方便的语言很有用。  
自定义分隔符不能包含空格或者等号。  

##版权
Mustache版权Copyright (C) 2009 Chris Wanstrath  
原始的CTemplate由Google开发  

