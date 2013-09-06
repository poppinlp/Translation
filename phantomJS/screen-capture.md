> 贡献者：梁鹏  
> 翻译时间：2013年8月31日  
> 原文来源：https://github.com/ariya/phantomjs/wiki/Screen-Capture  
> 原文作者：PhantomJS  
> 原文标题：Screen Capture  

#屏幕抓取

因为PhantomJS使用webkit内核，这是一个真实的布局和渲染引擎，所以它能像屏幕截图一样抓取网页。因为PhantomJS能渲染网页上的任何东西，所以它也能被用在除了HTML和CSS的其他地方，比如SVN和Canvas。

下面的脚本实现了一个简单的页面抓取。它读取了GITHUB的首页然后将它保存成`github.png`图片。

```
var page = require('webpage').create();
page.open('http://github.com/', function () {
    page.render('github.png');
    phantom.exit();
});
```

为了执行这个脚本，可以创建一个github.js文件保存上面的代码并放在phantomjs.exe同一个目录。然后在命令行中切换到该目录并执行下面的代码：

```
phantom.js github.js
```

除了PNG格式，PhantomJS也支持JPEG、GIT和PDF格式。

在`examples`子文件夹中有一个[rasterize.js](https://github.com/ariya/phantomjs/blob/master/examples/rasterize.js)脚本，它实现了一个更为完整的PhantomJS渲染特性。下面是一个利用该脚本基于SVG来渲染老虎的例子：

```
phantomjs rasterize.js http://ariya.github.com/svg/tiger.svg tiger.png
```

它将会生成下面的图片：

![老虎](https://github-camo.global.ssl.fastly.net/388d125df20fdb6cde57a23587b296151b4ac4d7/687474703a2f2f6c68362e67677068742e636f6d2f5f4f696a6866315a50762d342f545236694d384a304b72492f41414141414141414279342f52435a3845673536374c4d2f733430302f74696765722e706e67)

另一个例子是生成一个[极地时钟](http://raphaeljs.com/polar-clock.html)：

```
phantomjs rasterize.js http://raphaeljs.com/polar-clock.html clock.png
```

![极地时钟](https://lh5.googleusercontent.com/_Oijhf1ZPv-4/TUuUx1o-tuI/AAAAAAAAB00/Ba-Gxl5Zp6Q/s288/polar-clock.png)

生成一个PDF也很容易，例如来自一篇wikipedia的文章：

```
phantomjs rasterize.js 'http://en.wikipedia.org/w/index.php?title=Jakarta&printable=yes' jakarta.pdf
```

构造canvas也很简单，并且能被轻松的转换为图片。PhantomJS自带例子中的[colorwheel.js](https://github.com/ariya/phantomjs/blob/master/examples/colorwheel.js)就能生成如下的色轮：

![色轮](https://lh3.googleusercontent.com/-xSIzxPtJULw/TVzeP4NPMDI/AAAAAAAAB10/k-c8jB6I5Cg/s288/colorwheel.png)

用PhantomJS来提供网页截图服务是可行的。这里有一些能帮助你更容易实现这个服务的[项目](https://github.com/ariya/phantomjs/wiki/Related-Projects)。
