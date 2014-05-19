> 贡献者：梁鹏  
> 翻译时间：2014年5月19日  
> 原文来源：http://gruntjs.com/api/grunt  
> 原文作者：GruntJS  
> 原文标题：grunt  

#grunt
Grunt把所有的属性和方法都通过`grunt`对象暴露了出来，并把这个对象传递给了`module.exports`，方便在Gruntfile、插件或者任务中使用。

几乎下面所有的方法都是在别处定义的，但都可以直接通过`grunt`对象方便的访问到。可以通过看他们各自的API文档来获取详细的说明和例子。

##Config

###grunt.initConfig
这个方法是[grunt.config.init](http://gruntjs.com/grunt.config#grunt.config.init)方法的别名。

##Creaing Tasks

###grunt.registerTask
这个方法是[grunt.task.registerTask](http://gruntjs.com/grunt.task#grunt.task.registertask)方法的别名。

###grunt.registerMultiTask
这个方法是[grunt.task.registerMultiTask](http://gruntjs.com/grunt.task#grunt.task.registermultitask)方法的别名。

###grunt.renameTask
这个方法是[grunt.task.renameTask](http://gruntjs.com/grunt.task#grunt.task.renametask)方法的别名。

##Loading Externally-Defined Tasks

###grunt.loadTasks
这个方法是[grunt.task.loadTasks](http://gruntjs.com/grunt.task#grunt.task.loadtasks)方法的别名。

###grunt.loadNpmTasks
这个方法是[grunt.task.loadNpmTasks](http://gruntjs.com/grunt.task#grunt.task.loadnpmtasks)方法的别名。

##Warnings and Fatal Errors

###grunt.warn
这个方法是[grunt.fail.warn](http://gruntjs.com/grunt.fail#grunt.fail.warn)方法的别名。

###grunt.fatal
这个方法是[grunt.fail.fatal](http://gruntjs.com/grunt.fail#grunt.fail.fatal)方法的别名。

##Command-line Options

###grunt.option
取得命令行选项的值，例如`debug`。需要注意的是，对于任何命令行选项，它的否定值也是可以用来测试的，例如`no-debug`。

```
grunt.option(optionName)
```

##Miscellaneous

###grunt.package
是一个对象，里面保存着当前Grunt`package.json`里的信息。

```
grunt.package
```

###grunt.version
是一个字符串，表示当前Grunt的版本。这是`grunt.package.version`属性的简写。

```
grunt.version
```

