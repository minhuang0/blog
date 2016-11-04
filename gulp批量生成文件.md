title: gulp批量生成文件
date: 2016-09-19
tags: 
    - gulp
    - 自动化
categories: 编程

---

遇到一个问题，需要大批量的生成文件夹,每个文件夹目录下面的html内容都差不多，如果用人肉手动创建并修改这些html的话是做一些重复而且没有意义的事情。如下所示:

a.html
```
<html>
    ...
    <script>
        fun("1");
    </script>
</html>
```

里面的"1"是变化的,会对应生成 `a_1/index.html` `a_2/index.html` `a_3/index.html`等等，里面的`fun()`参数分别是`1`, `2`, `3`

使用gulp来进行创建这些文件夹,并自动修改这些规律的改动，能够省事不少。

主要使用到的是:

- [node-glob](https://github.com/isaacs/node-glob)
- [gulp-replace](https://github.com/lazd/gulp-replace)
- [gulp-rename](https://github.com/hparra/gulp-rename)

node-glob主要用于遍历文件,gulp-replace用于替换文件内容

整体思路:

遍历所有文件 --> 替换文件里面关键的内容 --> 生成文件和文件夹


