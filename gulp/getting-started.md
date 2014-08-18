> 贡献者：梁鹏  
> 翻译时间：2014年8月18日  
> 原文来源：https://github.com/gulpjs/gulp/blob/master/docs/getting-started.md  
> 原文作者：gulp  
> 原文标题：Getting Started  

# 快速入门

#### 1. 全局安装 gulp ：

```sh
$ npm install --global gulp
```

#### 2. 在你项目的依赖（devDependencies）中安装 gulp ：

```sh
$ npm install --save-dev gulp
```

#### 3. 在你项目的根目录创建一个 `gulpfile.js`：

```js
var gulp = require(‘gulp’);

gulp.task(‘default’, function() {
    // place code for your default task here
});
```

#### 4. 执行 gulp：

```sh
$ gulp
```

默认的任务将会执行，虽然它没有做任何事情。

想单独执行某些任务，可以使用 `gulp <task> <othertask>`。

## 接下来该做什么？

现在你有一个空的 gulpfile 并且安装好了所有东西。那么你如何真正的开始使用呢？可以看看这些[使用方法](https://github.com/gulpjs/gulp/blob/master/docs/recipes)和[介绍文章](https://github.com/gulpjs/gulp/blob/master/docs/README.md#articles)来获取更多信息。

## .src, .watch, .dest, CLI 参数 - 我该如何使用它们？

关于 CLI 参数，可以看看 [CLI文档](https://github.com/gulpjs/gulp/blob/master/docs/CLI.md)。关于 API 的内容，可以看看 [API文档](https://github.com/gulpjs/gulp/blob/master/docs/API.md)。

## 可用的插件

Gulp 的社区在不断成长中，每天都会有新的插件诞生。可以在[这个页面](http://gulpjs.com/plugins/)上看到完整的插件列表。
