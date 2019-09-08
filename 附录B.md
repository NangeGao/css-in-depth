# 附录B 预处理器

对于现代CSS工作流来讲，使用预处理器是必不可少的一部分。预处理器为提升代码书写效率提供了很多便利，而且有助于维护基础代码。举个例子，我们有时候只需要写几行代码，然后在整个样式表中复用它。

预处理器的工作原理是把我们写的源文件转译成标准CSS样式表。大部分情况下，源文件看上去和标准CSS差不多，只是增加了一些额外的特性。一个使用了预处理器变量的简单示例，看上去大概是这样的：

> [p422 代码片断一]

这段代码片断定义了一个名为`$brand-blue`的变量，用在了样式表后面的两个不同的地方。使用Sass预处理器运行的时候，整个样式表中的变量都被替换了，输出了下面的CSS：

> [p422 代码片断二]

我们需要明确一件事情，对于浏览器而言，因为最终输出是标准CSS，预处理器不会向语言添加任何新特性。但对于作为开发者的我们来讲，预处理器确实提供了许多方便。

在前面的例子中，使用变量代表颜色值，就可以多次重复使用它，而不需要每次复制粘贴十六进制码。生成输出文件的过程中，预处理器替我们做了重复复制这件事情。这也意味着我们可以在一个地方修改变量值，改动会传递到整个样式表。

预处理器有好几种，其中比较流行的两个是`Sass`（[https://sass-lang.com/](https://sass-lang.com/)）和`Less`（[http://lesscss.org/](http://lesscss.org/)）。Sass是最常见的预处理器，接下来我们会占用较多的篇幅来介绍它。Less和Sass其实比较类似，主要在一些语法细节上有所区别。举例来说，Sass使用$来表示变量（`$brand-blue`），而Less使用@符号（`@brand-blue`）。附录中提到的所有Sass特性，Less都支持，可以浏览Less的官方文档查看语法上的区别。

## B.1 Sass

使用Sass之前，需要先确定几件事情。首先是使用哪种实现方案。Sass是用Ruby写的，但这种实现方式在编译大型样式表的时候比较慢，所以建议使用`LibSass`，这是用C/C++实现的Sass编译器。

如果你对JavaScript和Node环境比较熟悉，可以通过npm包管理工具安装node-sass，也可以获取LibSass。如果还没有安装Node.js，可以在[https://nodejs.org](https://nodejs.org)上找到它（免费），按照上面的指导进行下载安装即可。后面会介绍相关的操作命令，但如果你想了解更多npm或者遇到问题需要求助，可以访问[https://docs.npmjs.com/getting-started/](https://docs.npmjs.com/getting-started/)。

### B.1.1 安装Sass

要安装Sass，先在终端中新建一个项目目录，并进入该目录。然后运行下面两条命令：

- `npm init -y`——初始化一个新的npm项目，创建package.json文件。关于该文件的更多信息可以查看第十章（10.1.1节）。
- `npm install --save-dev node-sass`——安装`node-sass`包，并把它作为开发依赖写入package.json。

> **注意**
>
> 在Windows系统中，还需要安装`node-gyp`包。更多信息可以查看[https://github.com/sass/node-sass#install](https://github.com/sass/node-sass#install)。

第二个需要确认的事情是使用哪种语法。Sass支持两种语法：Sass和SCSS。它们的语言特性是一样的，但Sass语法去掉了所有的花括号和分号，严格使用缩进来表示代码结构。比如：

> [p424 代码片断一]

这有点类似于Ruby和Python这样的编程语言，空格是有意义的。SCSS语法使用花括号和分号，所有看起来更像标准CSS。例如：