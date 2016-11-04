title: 使用Jade来共用重复代码
date: 2016-04-23
tags: 
  - html
  - Jade
categories: 编程

---
 
花了一些时间看了jade官网的[api](http://jade-lang.com/reference/attributes/)
<!--more--> 
，发现之前使用Titanium时写的jade就用到的其中的两个功能(羞愧)。

- Attributes,tags(漂亮的html排版，不需要`<>`、`</>` 使用代码缩进来控制层级)
- Includes(能够引入部分html代码嵌入页面，区分出一些功能模块)

这个官网的部分代码截图用的比我更好，才发现还能用 `include css` 文件:

![jade includes png](http://i.imgur.com/z9CUx8b.png)

<!-- more -->

jade github上面的介绍是: 

> Pug – robust, elegant, feature rich template engine for Node.js http://jade-lang.com

确实很强大，而且写起来很优雅。能够节省大量的html里面的闭标签，减少html阅读量，提高前端每行代码的单价。

还是的提一下，Jade使用缩进，所以各位使用Vim,SubLime Text最好是将自己的`tab` 键调整为x(我的习惯是4)个空格,避免编译的时候遇到缩进的问题。

下面是我对于几个特性的理解:

[extend](http://jade-lang.com/reference/extends/): 能够继承一段html code,并使用其中的将 `code` 传入到 被继承页面的  `block` 引用中。
[Template inheritance](http://jade-lang.com/reference/inheritance/) 模板继承也能够使用extend中的特性。

![enter image description here](http://i.imgur.com/3WLkfCS.png)


[Mixins](http://jade-lang.com/reference/mixins/): 类似于js中一个公共的方法，使用调用这个方法并传入参数会返回一些预先设定好的 block ;

![enter image description here](http://i.imgur.com/QdzNfyL.png)

case,conditionals，code,[Iteration](http://jade-lang.com/reference/iteration/): 能够使用 `swich case`  , `if else`  , `while` , `for` , `each` 等语句和 `+ ` 字符串加运算。

需要注意的是加上**!**后会不会解析字符串中的`<html>` 标签。如下图:

```jade
p!= 'This code is' + ' <strong>not</strong> escaped!'
```

其余还有一些特性如下:

- [comment](http://jade-lang.com/reference/comments/)(jade中的代码行注释,块注释，开发环境下的配置)
- [Filters](http://jade-lang.com/reference/filters/)(将一些其他语言如markdown,coffee-script转码)
- [Interpolation](http://jade-lang.com/reference/interpolation/)(能够像ng,react一样能够传入一些变量到html中)
- [Plain Text](http://jade-lang.com/reference/plain-text/)(在jade中输入纯文本)

Jade能够拆分比较大的页面，能够将公共的html封装并达到重复引用的作用。在开发过程中可以通过命令行的形式让其自动检测变化并编译，或者通过一些自动化工具来达到同样的效果。如gulp,webpack等。