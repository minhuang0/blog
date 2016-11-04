title: nodejs笔记
date: 2016-01-05
tags: 
    - nodejs

---

学习[地址](https://github.com/alsotang/node-lessons)
<!--more--> 
# 工具

node的版本管理工具:NVM(Node Version Manager)([https://github.com/creationix/nvm](https://github.com/npm/npm))

node包管理工具:npm(node package manage)([https://github.com/npm/npm](https://github.com/npm/npm))


npm修改淘宝源: 添加代码`registry = https://registry.npm.taobao.org`到~/.npmrc

`npm init`: 初始化package.json
`npm install --save`: 安装包并将包版本名称写入package.json
`--save-dev`: 安装可执行的包在本地



# 包

[express](http://expressjs.com): web框架

引入依赖 `var express = require('express');`
require对应与express中的`module.exports` or `exports`(两者之间的区别),此时得到的`express`并不是实例对象,个人理解为是一段可执行的code。
`var app = express();`

此时的app才是一个express实例

[superagent](http://visionmedia.github.com/superagent/): 类Ajax组件

[cheerio](http://cheeriojs.github.io/cheerio/): 类jquery组件


[eventproxy](https://github.com/JacksonTian/eventproxy): 事件异步处理

[asyac](https://github.com/caolan/async): 控制并发的工具


[mocha](http://mochajs.org/):测试框架

[should](https://github.com/tj/should.js): 断言库

[chai](http://chaijs.com/): 全栈断言库

[istanbul](https://github.com/gotwarlost/istanbul): 测试率覆盖工具

[nodemon](https://github.com/remy/nodemon):Node的监测文件改动并自动编译

[phantomjs](http://phantomjs.org/): 浏览器测试工具

[supertest](https://github.com/tj/supertest): 所有兼容 connect 的 web 框架进行集成测试(配合express)


