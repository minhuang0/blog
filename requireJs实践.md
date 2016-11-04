title: requireJs实践
date: 2016-07-31
tags: 
    - javascript
    - requireJs
categories: 编程

---

最近维护公司的项目，由于项目加载的js过多，拖慢了页面打开速度，同时页面中的js也存在各种依赖，想用模块化工具来维护js加载顺序。

[demo](http://www.huangmin.me/demo/html/requireJsDemo/require.html)

<!--more-->  

### require做了什么

require的目的是为了是页面加载速度更快加载js文件更少并能够处理好文件依赖。
实现原理是将在html中使用script引入的多个js文件变成一个入口js文件，并通过路径的方式来取的文件并按照模块化的方式分别将不同的js引入并处理之间的依赖关系，实现文件无阻塞引入。

### 使用require
首先新建一个简单的html页面:

require.html:

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>require js Demo</title>
    <script data-main="main.js" src="require.js"></script>
</head>
<body>
    <h1>I'm require js Demo</h1>
</body>
</html>
```

`<script data-main="main.js" src="require.js"></script>`中src是require js的路径,而main.js是入口。也就是说我们需要在main.js里面处理和引入项目中需要的其他js文件。

下面定义了一个math的模块,里面有add function

math.js: 

```
//AMD规范(什么是AMD 参考:http://www.requirejs.cn/docs/whyamd.html)是使用define()方法来进行函数定义,下面定义了一个add方法，并将包含add function的obj返回出去
define(function() {
    var add = function(x, y) {
        return x + y;
    };
    console.info("load math js");
    return {
        add: add
    };
});

```

上面的math是由AMD规范封装的，所以我们现在在main.js里面正确的引用math这个模块:

math.js

```
require(['math'], function(math){
    console.info(math.add(1, 2)); //6
});
```

require('math'),并以math作为参数传递进去。
当我们想引入外部的js文件时,下面以JQuery为例,下面介绍了require config 中paths,shim的作用。

重新修改main.js:

```
// require.config 中 paths是指给特定url的js文件取一个别名(like unix alias)
require.config({
    paths: {
        // 加上数组是为了防止第一个url中js加载不出来而采用第二种url方式加载
        "jquery": ["https://cdn.bootcss.com/jquery/3.1.0/jquery.min", "js/jquery.3.1.0.min"],
        // 如果是单个可以不需要加数组,例如: "markded": "https://cdn.bootcss.com/marked/0.3.5/marked.min"
    }
    // 我们可以给require的路径指向默认的路径，此时如果改为js/lib,则require('math')则实际内容是require('js/lib/math')
    // baseUrl: "js/lib", 
    // shim能让require加载非规范模块(不符合AMD规范的),使用`deps`能够指定该模块指定依赖,exports则是给该模块添加别名,类似于alias一样，使用underscore时能用_调用。
    /* shim: {
        'underscore': {
            exports: '_'
        },
        'backbone': {
            deps: ['underscore', 'jquery'],
            exports: 'Backbone'
        }
    }
    */
});
// 下面加载了 math, jquery, marked三个模块，并将 `math, $` 当做参数传递,调用了math.add function 和jqueryObj append的function
require(['math', "jquery"], function(math, $) {
    $('body').append('<p>1 + 2 = ' + math.add(1, 2) + ';</p>');//此时页面出现了1 + 2 = 3
});
```

### 总结

在只需要处理js依赖的情况下使用requirejs或者seajs这个工具能够合理并且清晰的管理js文件依赖。如果还想要打包css,image等source文件时,也可以可以采用webpack来构建开发。