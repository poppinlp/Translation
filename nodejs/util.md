> 贡献者：梁鹏  
> 翻译时间：2014年4月7日  
> 原文来源：http://www.nodejs.org/api/util.html  
> 原文作者：NodeJS  
> 原文标题：Util  

#Util
> Stability: 4 - API Frozen

这些函数都在`util`模块中，可以使用`requir('util')`来引用。

##util.format(format, [...])
像`printf`一样根据第一个参数返回一个格式化的字符串。

第一个参数是一个包含零个或者更多占位符的字符串。每一个占位符将被替换为对应参数转换后的值。支持的占位符有：

- %s - 字符串 
- %d - 数字 (整数和浮点数都行)
- %j - JSON
- % - 单独的百分号，不会被参数替换

如果占位符没有与之对应的参数，那么不会被替换。

```
util.format('%s:%s', 'foo'); // 'foo:%s'
```

如果参数的数量大于占位符的数量，多余的参数将会被`util.inspect()`转换为字符串，并且由空格分割与前面的字符串级联。

```
util.format('%s:%s', 'foo', 'bar', 'baz'); // 'foo:bar baz'
```

如果第一个参数不是格式化的字符串，那么`util.format()`将返回所有参数以空格分隔的级联字符串，其中每个参数都会由`util.inspect()`转换。

```
util.format(1, 2, 3); // '1 2 3'
```

##util.debug(string)
一个同步的输出函数，将会阻塞进程并且立刻输出`string`到`stderr`。

```
require('util').debug('message on stderr');
```

##util.error([...])
和`util.debug()`一样，只是这个函数会立刻输出所有的参数到`stderr`。

##util.puts([...])
一个同步的输出方法，将会阻塞进程并且输出所有参数到`stdout`，每个参数的结尾都会换行。

##util.print([...])
一个同步的输出方法，将会阻塞进程，将每个参数转换为字符串并输出到`stdout`，参数的结尾不会换行。

##util.log(string)
将`string`和时间戳一起输出到`stdout`。

```
require('util').log('Timestamped message.');
```

##util.inspect(object, [options])
返回`object`的字符串呈现，主要是用来调试的。

可选的`options`参数可以用来改变格式化字符串的某些方面：

- `showHidden` - 如果为`true`，那么对象中不能枚举的属性也会被显示。默认为`false`。
- `depth` - 用来告诉`inspect`在格式化对象的时候需要递归多少次，这对于一些复杂的对象非常实用。默认为`2`。如果想无限制递归的话可以实用`null`。
- `colors` - 如果为`true`，那么输出将会被应用上ANSI代码颜色。默认为`false`。颜色定制的方式下面会讲。
- `customInspect` - 如果为`false`，那么在被格式化的对象上自定义的`inspect()`方法将不会被调用。默认为`true`。

这是个格式化输出所有`util`对象属性的例子：

```
var util = require('util');
console.log(util.inspect(util, { showHidden: true, depth: null }));
```

##Customizing util.inspect colors
通过`util.inspect`输出内容的颜色（如果激活了）是通过全局对象`util.inspect.styles`和`util.inspect.colors`定义的。

`util.inspect.styles`中每个样式的颜色是与`util.inspect.colors`匹配对应的。高亮和它们默认的颜色匹配为：`number` (yellow) `boolean` (yellow) `string` (green) `date` (magenta) `regexp` (red) `null` (bold) `undefined` (grey) `special` - only function at this time (cyan) * name (intentionally no styling)

Predefined color codes are: `white`, `grey`, `black`, `blue`, `cyan`, `green`, `magenta`, `red` and `yellow`. There are also `bold`, `italic`, `underline` and `inverse` codes.

Objects also may define their own `inspect(depth)` function which `util.inspect()` will invoke and use the result of when inspecting the object:

```
var util = require('util');

var obj = { name: 'nate' };
obj.inspect = function(depth) {
    return '{' + this.name + '}';
};

util.inspect(obj);
// "{nate}"
```

##util.isArray(object)
如果参数是个`Array`，那么返回`true`，否则返回`false`。

##util.isRegExp(object)
如果参数是个`RegExp`，那么返回`true`，否则返回`false`。

##util.isDate(object)
如果参数是个`Date`，那么返回`true`，否则返回`false`。

##util.isError(object)
如果参数是个`Error`，那么返回`true`，否则返回`false`。

##util.inherits(constructor, superConstructor)
从一个构造函数继承原型方法给另一个。`constructor`的原型将会被设置为来自`superConstructor`的新的对象。

另一个方便之处就是可以通过`constructor.super_`属性访问到`superConstructor`。

```
var util = require("util");
var events = require("events");

function MyStream() {
    events.EventEmitter.call(this);
}

util.inherits(MyStream, events.EventEmitter);

MyStream.prototype.write = function(data) {
    this.emit("data", data);
}

var stream = new MyStream();

console.log(stream instanceof events.EventEmitter); // true
console.log(MyStream.super_ === events.EventEmitter); // true

stream.on("data", function(data) {
    console.log('Received data: "' + data + '"');
})
stream.write("It works!"); // Received data: "It works!"
```
