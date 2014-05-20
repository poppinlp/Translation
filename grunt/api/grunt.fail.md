> 贡献者：梁鹏  
> 翻译时间：2014年5月19日  
> 原文来源：http://gruntjs.com/api/grunt.fail  
> 原文作者：GruntJS  
> 原文标题：grunt.fail  

#grunt.fail

用来处理一些严重错误。可以在[fail lib source](https://github.com/gruntjs/grunt/blob/master/lib/grunt/fail.js)中查看更多信息。

##The fail API
在任务中，如果有东西崩溃了或者即将崩溃，这回强制让Grunt中止。可以在[exit codes documentation](https://github.com/poppinlp/Lranslation/blob/master/grunt/api/exit-codes.md)中查看Grunt内置的退出代码列表。

注意，下面方法中标注了`ALL`的是可以直接在`grunt`对象上使用的，使用的别名在标注在等号后，可以在[API main page](https://github.com/poppinlp/Lranslation/blob/master/grunt/api/grunt.md)查看更多信息。

###grunt.fail.warn [ALL = grunt.warn]
展示一个警告并立即中止Grunt。如果命令行选项提供了`--force`，那么Grunt将会继续执行。`error`参数可能是一个字符串或者是一个错误对象。

```js
grunt.fail.warn(error [, errorcode])
```

如果命令行选项提供了`--stack`并且存在错误对象，那么将会打印出错误堆栈。

###grunt.fail.fatal [ALL = grunt.fatal]
展示一个警告并立即中止Grunt。`error`参数可能是以讹过字符串或者是以讹过错误对象。

```js
grunt.fail.fatal(error [, errorcode])
```

如果命令行选项提供了`--stack`并且存在错误对象，那么将会打印出错误堆栈。

如果没有提供`--no-color`参数，那么在报错时将会发出一个响声。
