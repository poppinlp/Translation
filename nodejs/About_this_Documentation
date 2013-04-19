1.关于本文档
    这篇文档的目的是从概念和参考两个方面给予nodejs API一个比较全面的介绍。每一个内置的模块或者高级概念都会有一个段落来介绍。
    对于每一个属性、方法和事件的参数，都会在该话题的标题下面有一个准确而详细的列表。
    每一个.html文档都会有一个与之对应的以结构化的方式呈现相通信息的.json文档。这个特性只是实验性的，并且它是由IDE和其他希望通过这个文档来进行编程相关的事情的应用程序提供的。
    每一个.html和.json文件都是通过node源代码里doc/api/目录下的与之对应的.markdown文件生成的。文档是通过tools/doc/generate.js生成的。html模板位于doc/template.html。


2.稳定性
    贯穿文档，你能看到不同章节的稳定性的显示。nodejs API仍然在不断微调，但在它成熟的过程中，有些部分是更可靠的。比如一些已经被证明并且作为基础被依赖的部分，它们不太可能有更改。而另一些则可能是新的、实验性的、有危险性的或者是正在被重新设计。
    具体稳定性指数如下：
    Stability: 0 - Deprecated
    This feature is known to be problematic, and changes are
    planned.  Do not rely on it.  Use of the feature may cause warnings.  Backwards
    compatibility should not be expected.

    Stability: 1 - Experimental
    This feature was introduced recently, and may change
    or be removed in future versions.  Please try it out and provide feedback.
    If it addresses a use-case that is important to you, tell the node core team.

    Stability: 2 - Unstable
    The API is in the process of settling, but has not yet had
    sufficient real-world testing to be considered stable. Backwards-compatibility
    will be maintained if reasonable.

    Stability: 3 - Stable
    The API has proven satisfactory, but cleanup in the underlying
    code may cause minor changes.  Backwards-compatibility is guaranteed.

    Stability: 4 - API Frozen
    This API has been tested extensively in production and is
    unlikely to ever have to change.

    Stability: 5 - Locked
    Unless serious bugs are found, this code will not ever
    change.  Please do not suggest changes in this area; they will be refused.


3.json输出
    Stability: 1 - Experimental
    每一个html文件都有一个包含同样数据的使用markdown的与之对应的json文件。
    这个特性是在node v0.6.12中加入的。目前仍是实验性的。
