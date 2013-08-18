> 贡献者：梁鹏  
> 翻译时间：2013年8月16日  
> 原文来源：http://www.nodejs.org/api/documentation.html  
> 原文作者：NodeJS  
> 原文标题：About this Documentation  

#关于这一系列文档
这一系列文档的目的是从概念和使用两个方面给予nodejs API一个比较全面的介绍。每一个内部模块或者高级概念都会有一个段落来介绍。  
对于每一个属性类型、方法参数和事件参数，都会在该话题的顶部下面有一个准确而详细的列表。  
每一个html文档都会有一个与之对应的以结构化的方式呈现相同内容的json文档。这个特性只是实验性的，主要是为了IDE或其他希望通过这个文档来进行编程相关的事情的程序提供的。  
每一个html和json文档都是由node源代码里`doc/api/`目录下的与之对应的markdown文件生成的。文档的生成使用了`tools/doc/generate.js`，其中使用到的html模板是`doc/template.html`。

##稳定性
贯穿整个文档，你能看到不同章节的稳定性的显示。nodejs API仍然在不断微调，但在它成熟的过程中，有些部分是更可靠的。比如一些已经被验证并且作为基础被依赖的部分，它们不太可能有更改。而另一些则可能是新的、实验性的、有危险性的或者是正在被重新设计。  
具体稳定性指数和含义如下：（这部分我就不翻译了）

> Stability: 0 - Deprecated  
> This feature is known to be problematic, and changes are planned. Do not rely on it. Use of the feature may cause warnings. Backwards compatibility should not be expected.  
> Stability: 1 - Experimental  
> This feature was introduced recently, and may change or be removed in future versions. Please try it out and provide feedback. If it addresses a use-case that is important to you, tell the node core team.  
> Stability: 2 - Unstable  
> The API is in the process of settling, but has not yet had sufficient real-world testing to be considered stable. Backwards-compatibility will be maintained if reasonable.  
> Stability: 3 - Stable  
> The API has proven satisfactory, but cleanup in the underlying code may cause minor changes. Backwards-compatibility is guaranteed.  
> Stability: 4 - API Frozen  
> This API has been tested extensively in production and is unlikely to ever have to change.  
> Stability: 5 - Locked  
> Unless serious bugs are found, this code will not ever change. Please do not suggest changes in this area; they will be refused.  

##json输出
> Stability: 1 - Experimental

每一个html文件都有一个包含同样数据的使用markdown的与之对应的json文件。  
这个试验性的特性是在node v0.6.12中加入的。
