> 贡献者：梁鹏  
> 翻译时间：2014年5月20日  
> 原文来源：http://gruntjs.com/api/grunt.util  
> 原文作者：GruntJS  
> 原文标题：grunt.util  

#grunt.util
为Gruntfile和任务提供了各种各样的通用工具。

##grunt.util.kindOf
返回值的类型。类似于`typeof`但返回其内部的`[[Class]]`值。可能的返回值有`"number"`, `"string"`, `"boolean"`, `"function"`, `"regexp"`, `"array"`, `"date"`, `"error"`, `"null"`, `"undefined"`和通用的`"object"`。

```js
grunt.util.kindOf(value)
```

###grunt.util.error
返回一个包含错误信息的可以被抛出的错误对象实例。如果已经提供了一个代替`message`的错误对象，那么将返回那个对象。

如果提供了一个代替`origError`的错误对象，并且Grunt在`--stack`参数下运行，那么将会打印出原始的错误堆栈信息。

```js
grunt.util.error(message [, origError])
```

###grunt.util.linefeed
代表符合当前操作系统的换行符。（对于Windows是`\r\n`，对于其他系统是`\n`）

###grunt.util.normalizelf
返回将参数字符串规范化换行符之后的结果。（对于Windows是`\r\n`，对于其他系统是`\n`）

```js
grunt.util.normalizelf(string)
```

###grunt.util.recurse
对于嵌套的对象和数组中的值，递归的执行`callbackFunction`。如果`continueFunction`返回`false`，那么那个对象或者值将被跳过执行。

```js
grunt.util.recurse(object, callbackFunction, continueFunction)
```

###grunt.util.repeat
返回将`str`字符串`n`次循环后的字符串。

```js
grunt.util.repeat(n, str)
```

###grunt.util.pluralize
提供类似`"a/b"`形式的字符串`str`，如果`n`是`1`那么返回`a`，否则返回`b`。如果你使用的不是'/'，也可以自行指定分隔符。

```js
grunt.util.pluralize(n, str, separator)
```

###grunt.util.spawn
开启一个新的子进程，跟踪它的标准输出流、标准错误流和结束代码。该方法返回开启的子进程的引用。当子进程退出的时候，`doneFunction`会被调用。

```js
grunt.util.spawn(options, doneFunction)
```

`options`对象可能有这些属性：

```js
var options = {
  // The command to execute. It should be in the system path.
  cmd: commandToExecute,
  // If specified, the same grunt bin that is currently running will be
  // spawned as the child command, instead of the "cmd" option. Defaults
  // to false.
  grunt: boolean,
  // An array of arguments to pass to the command.
  args: arrayOfArguments,
  // Additional options for the Node.js child_process spawn method.
  opts: nodeSpawnOptions,
  // If this value is set and an error occurs, it will be used as the value
  // and null will be passed as the error value.
  fallback: fallbackValue
};
```

`doneFunction`接受这些参数：

```js
function doneFunction(error, result, code) {
  // If the exit code was non-zero and a fallback wasn't specified, an Error
  // object, otherwise null.
  error
  // The result object is an object with the properties .stdout, .stderr, and
  // .code (exit code).
  result
  // When result is coerced to a string, the value is stdout if the exit code
  // was zero, the fallback if the exit code was non-zero and a fallback was
  // specified, or stderr if the exit code was non-zero and a fallback was
  // not specified.
  String(result)
  // The numeric exit code.
  code
}
```
