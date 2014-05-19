> 贡献者：梁鹏  
> 翻译时间：2014年5月19日  
> 原文来源：http://gruntjs.com/api/grunt.config  
> 原文作者：GruntJS  
> 原文标题：grunt.config  

#grunt.config
用来获取Gruntfile中定义的项目配置信息。

注意，下面方法中标注了`ALL`的是可以直接在`grunt`对象上使用的，标注了`THIS`的是可以在任务中通过`this`对象使用的，使用的别名在标注在等号后。

##Initializing Config Data

###grunt.config.init [ALL = grunt.initConfig]
用来对当前项目初始化配置对象。提供的`configObject`参数可以在任务中通过`grunt.config`方法获取到。几乎所有的项目的`Gruntfile`都会调用这个方法。

```
grunt.config.init(configObject)
```

注意，在配置信息被检索的时候，任何提供的`<% %>`模版字符串都会被执行。

下面是一个[grunt-contrib-jshit插件](https://github.com/gruntjs/grunt-contrib-jshint)`jshit`任务的配置信息例子：

```
grunt.config.init({
    jshint: {
        all: ['lib/*.js', 'test/*.js', 'Gruntfile.js']
    }
});
```

可以在[Getting started](http://gruntjs.com/getting-started/)中找到更多配置的例子。

##Accessing Config Data

