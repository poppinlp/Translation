> 贡献者：梁鹏  
> 翻译时间：2014年8月24日  
> 原文来源：https://github.com/gulpjs/gulp/blob/master/docs/CLI.md  
> 原文作者：gulp  
> 原文标题：gulp CLI docs  

## gulp CLI 文档

### 参数

在 gulp 中需要了解的参数并不多，其它很多参数都是在需要时给任务使用的。

- `-v` 或者 `--version` 将会显示全局和本地的 gulp 版本号
- `--require <module path>` 将会在 gulpfile 执行前加载模块。这在需要引入其他插件的时候非常游泳。你可以使用多个 `--require`。
- `--cwd <dir path>` 手动设置当前工作目录(current working directory)。搜索 gulpfile 和 加载模块的相对路径都会从这里开始寻找。
- `--gulpfile <gulpfile path>` 手动设置 gulpfile 的路径。当你有多个 gulpfiles 的时候会很有用。这也会把 CWD 更改为 gulpfile 所在的目录。
- `-T` or `--tasks` 这会显示已加载的 gulpfile 中的任务依赖树
- `--tasks-simple` 这会显示已加载的 gulpfile 中的任务列表
- `--color` 这会强制 gulp 和它的插件展示颜色，甚至在已知没有支持的颜色时也会这样
- `--no-color` 这会强制 gulp 和它的插件不展示颜色，甚至在已知有支持的颜色时也会这样
- `--silent` 这会关掉所有 gulp 的日志记录

CLI 会自动将其执行的路径添加到 process.env.INIT_CWD。

### 任务

可以通过 `gulp <task> <othertask>` 来执行任务。如果只执行 `gulp`，那将会执行你注册为 `default` 的的任务。如果没有 `default` 任务，那么 gulp 将会报错。

### 编译器

你可以在这个[说明文档](https://github.com/tkellen/node-interpret#jsvariants)中找到目前支持的语言列表。如果你想增加更多的语言支持，请发 pull request 或者创建 issues。
