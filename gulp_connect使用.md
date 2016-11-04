title: 使用gulp_connect开启server
date: 2016-07-15
tags: 
    - gulp
categories: 编程

---

本文中提到的是[gulp-connect](https://github.com/AveVlad/gulp-connect)这个gulp插件，能够在开发web项目的时候，开启一个本地server,并监听文件的改动，自动刷新网页。对于我来说，一保存就能够自动刷新浏览器，少按了一次Ctrl + R刷新页面是很爽的。

安装步骤:

```
npm install --save-dev gulp
npm install --save-dev gulp-connect
```

至于为什么要安装在本地而不是全局的，在[stackoverflow](http://stackoverflow.com/questions/22115400/why-do-we-need-to-install-gulp-globally-and-locally)上面有个很好的回答，大概意思指安装在全局的时候共用一个命令,给项目带来了更多依赖。而安装在本地有package.json来保存项目该用的版本信息，在npm安装的时候会先搜索本地全局是否存在才会去远程下载。
<!--more-->  

`--save-dev` 指保存在package.json中并能够直接在本地调用

首先要引入gulp和gulp-connect

```javascript
var gulp = require('gulp'),
  connect = require('gulp-connect');
```

定义启动server任务,root是目录路径，livereload则是用来自动刷新

```javascript
gulp.task('connect', function() {
  connect.server({
    root: 'app',
    livereload: true
  });
});

```

还需要定义监听页面的文件变化和让connect刷新的任务,src指文件路径，`/**/*html` 指任任意名字任意个数下的html,js文件

```javascript
gulp.task('html', function () {
  gulp.src(['./app/**/*.html','./app/**/*.js'])
    .pipe(connect.reload());
});

gulp.task('watch', function () {
  gulp.watch(['./app/**/*.html','./app/**/*.js'], ['html']);
});

```

最后将gulp的default命令来启动connect和watch这两个任务。

```javascript
var gulp = require('gulp'),
  connect = require('gulp-connect');

gulp.task('connect', function() {
  connect.server({
    root: 'app',
    livereload: true
  });
});

gulp.task('html', function () {
  gulp.src(['./app/**/*.html','./app/**/*.js'])
    .pipe(connect.reload());
});

gulp.task('watch', function () {
  gulp.watch(['./app/**/*.html','./app/**/*.js'], ['html']);
});

gulp.task('default', ['connect', 'watch']);
```

这时候能够启动端口在 `:8080`并将app目录下的html,js文件做了监听，文件发生改变时则重新加载浏览器页面。