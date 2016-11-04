title: webpack和react踩坑笔记
date: 2016-08-01
tags: 
    - webpack
    - react
categories: 编程

---



### 第一次看webpack

第一次看webpack是在2016-01-18,那时候看不是很明白，对于自动化打包没有接触过，按照webpack官网中的教程走了一遍。

[webpack getting started](http://webpack.github.io/docs/tutorials/getting-started/)

![引用图片](http://webpack.github.io/assets/what-is-webpack.png)

<!--more-->

### 安装:

在终端中输入命令: `npm install webpack -g`


一个简单的配置文件如下`webpack.config.js`:

```json

module.exports = {
    entry: "./entry.js",
    output: {
        path: __dirname,
        filename: "bundle.js"
    },
    module: {
        loaders: [
            { test: /\.css$/, loader: "style!css" }
        ]
    }
};
```


entry: 入口地址

output: 输出地址
    path： 加载的目录地址 
    filename: 生成的目标文件

loaders: 模块加载器

    如`{ test: /\.css$/, loader: "style!css" }`是用于处理样式文件的加载器

开发模式下的监听文件变化:

```
webpack --watch
```

启动一个server在[8080端口](http://localhost:8080/webpack-dev-server):

```
npm install webpack-dev-server -g
webpack-dev-server --progress --colors
```


接在在webpack环境准备好后安装react

install react: 
```
npm install react --save
```

使用react在编写jsx或js的文件是需要引用

```
import React from "react";
import { render } from 'react-dom'; //调用了这里为了方便直接将render引入进来了,就不需要ReactDom.render方法
```

在编写代码的时候会用到es6,scss，于是还添加了babel,sass的loaders

```
module: {
    loaders: [{
        test: /\.js|jsx$/,
        exclude: /(node_modules|bower_components)/,
        loader: 'babel',
        query: {
            presets: ['react', 'es2015']
        }
    }, {
        test: /\.css$/,
        loader: "style!css"
    }, {
        test: /\.scss$/,
        loader: "style!css!sass"
    }, {
        test: /\.(jpg|png)$/,
        loader: "url?limit=8192"
    }]
}
```

在jsx中引入scss可以使用require的方式

```
require("../css/comm.scss");
```

目前遇到问题：

- jquery和jquery-ui的引用问题
- react-router跳转问题
    - 我用的一种比较笨的方式
    ```
    this.props.history.replaceState(null,"/home");
    ```

需要去了解的内容:

- react-router
- redux配合react使用