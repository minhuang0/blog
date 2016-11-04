title: windows安装sass
date: 2016-09-03
tags: 
    - sass
categories: 编程

---

最近在windows下构建gulp的工作流,gulp主要处理sass的编译和合并, js的合并，images的压缩以及合成精灵图，以及启动服务和监听这些内容。

在安装sass的过程中遇到了很多报错提示的,如找不到 python、 visual C++、NET Framework;  not a win application等等

<!-- more -->

## 一些错误解决方案

- 网络条件不好，替换[源地址](http://www.huangmin.me/2016/08/25/npm%E5%A6%82%E4%BD%95%E6%94%B9%E5%8F%98%E6%BA%90%E5%9C%B0%E5%9D%80/)或者用淘宝的cnpm安装,或者网络条件好的情况下在安装。

- 安装时候的出现下面的error也是在安装的时候下载文件不完整造成的

```
Error: %1 is not a valid Win32 application.
```

重新安装的时候可以先清除本地node_modules下的node-sass

```
npm rm node-sass
npm install node-sass
```

- 当安装node的时候是用管理员权限安装的话,在安装node-sass也同时需要,不建议安装node时使用管理员权限（以及linux 使用 sudo）,可以安装nvm来安装node.

- node-sass 和 ruby-sass的区别

参考的这篇[文章](https://segmentfault.com/a/1190000003112509)

ruby-sass，依赖ruby环境,在编译的时候需要生成临时目录和临时文件。安装方式:

```
gem install sass
```

对应的gulp封装组件:

```
npm install gulp-ruby-sass
```


node-sass，依赖于nodejs 编译过程不需要临时目录和文件，直接通过buffer内容转换。

```
npm install node-sass 
```

对应的gulp封装组件:

```
npm install gulp-sass
```

在使用ruby-sass的时会生成缓存文件,在sass编译完成后会把临时文件清除，当后面有sass文件依赖于前面编译的文件时，则会读取不到改文件导致出错。

在使用node-sass的过程中，也碰到了当我在一个scss文件里面引入其他组件的scss文件的情况下，修改组件的scss文件,会提示该文件没找到，问题[issues](https://github.com/dlmanning/gulp-sass/issues/1#issuecomment-244533737)。原因是用的sublimeText的问题,需要设置subime Text

```
Preferences > Settings - User > "atomic_save": true
```

- gulp-sass中的配置

```
gulp.task('styles', function() {
    return gulp.src('src/sass/main.scss')
        .pipe(sass({includePaths : ['src/sass']}))
        .on('error', function(err) {
            console.error('Error!', err.message);
        })
        .pipe(autoprefixer({
            browsers: ['last 2 version', 'safari 5', 'ie 8', 'ie 9', 'opera 12.1', 'ios 6', 'android 4', 'Firefox < 20'],
            cascade: true,
            remove: true
        }))
        .pipe(minifycss())
        .pipe(gulp.dest('dist/css'))
        .pipe(connect.reload());
});
```

`gulp.src` 指的是目标路径（编译的文件）
`sass` 指的编译上述路径的文件
`includePaths`: 包含指定目录的sass文件（我在这里加上是避免在修改目标文件里面import其他scss文件时找不到文件的BUG。)
`autoprefixer`: 自动为代码加上浏览器兼容的前缀如`-webkit-`,`-moz-`
`minifycss` : 压缩生成后的css文件
`gulp.dest`: 输入目录
`connect.reload()`: 刷新本地的service