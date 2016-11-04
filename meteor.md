title: Meteor实践
date: 2015-12-29
tags: 
    - meteor

categories: 编程

---

[meteor](https://github.com/meteor/meteor/)
<!-- more -->

学习了一下meteor，照着教程写了一个[Demo](http://huangmin.meteor.com/)。

有一些收获,实时响应功能觉得很不可思议,在多个浏览器中能够同步响应,模版功能解决了一些重复布局代码。

Meteor的模版系统**[Spacebars](https://github.com/meteor/meteor/blob/devel/packages/spacebars/README.md)**:
	

- Inclusion: 可以使用 > `templateName` 来引入模版,类似于include某个文件
- Expression: 可以使用 `title 引用变量`,和angular有写类似
- Block Helper: 能够使用`#each.../each` 这样的语法块

meteor依赖跟踪**Computations**(没看明白,觉得很神奇)。

发布与订阅我觉得是能够由`client`决定想要什么,`servers`决定给什么东西。

延迟补偿（**Latency Compensation**）的概念,先让`client`改变,再`servers`改变,数据库保存后再给前台改变,但这时候就明显变化不大了。

我理解**Meteor Package**是一些封装好的功能,能够快速使用,同时也能自己发布一些包供别人下载。

