title: alloy team的编程规范
date: 2015-07-16
tags: 
    - css
    - html
categories: 编程

---

最近在维护公司已有项目的时候,发现每个人都有不同的代码书写风格,从文件命名到变量命名,注释到模块封装，就像战国时代百家争鸣一样。找文档看别人的团队是怎么统一规范的，加以学习借鉴。

在阅读的过程中也发现自己在写的过程中也有一些不是主流。
我的个人理解是标准规范不一定是100%正确的,讲个笑话`{` ***换行派*** 与 ***不换行派***。
每个人都也许能说出理由说自己这种书写方式的优点，
但我觉得 ***在某种程度上遵从世界上多数程序员及大牛的书写规范，在与人协同工作时,提交开源代码时,互相code review时都有一定程度的帮助与增加编码幸福感。***

原文[Code Guide by @AlloyTeam](https://github.com/AlloyTeam/CodeGuide)写的更全面,这里做自省和记录。

<!-- more -->

### 文件及文件夹命名

- project_name
- file_folder plural(scripts,styles)
- js_file.js 
- css_file.js
- html_file.js

### 共同地方

- soft tab（4个空格）

### HTML

- 属性小写内容双引号,自动闭合标签([HTML规范](https://dev.w3.org/html5/spec-author-view/syntax.html#syntax-start-tag))结尾不加 `/` 

```
<img src="images/company_logo.png" alt="Company">
```

- lang属性指定[语言](https://msdn.microsoft.com/en-us/library/ms533052.aspx)
- 编码 `<meta charset="UTF-8">`
- IE兼容模式 `<meta http-equiv="X-UA-Compatible" content="IE=Edge">`
- 引入js和css时不需要加`text/css` 和 `text/javascript`,HTML5规范定为默认的
- 属性顺序
    - class
    - id
    - name
    - data-*
    - src, for, type, href, value , max-length, max, min, pattern
    - placeholder, title, alt
    - aria-*, role
    - required, readonly, disabled
- boolean属性的存在表示取值为true，不存在则表示取值为false

### CSS,SCSS

- 属性 `0.5 -> .5`, `0px -> 0` , `border: 0 -> border: none`
- `{` `}` `>` `+` `/*` `*/`类似于js中运算符前后空格
- `}`、文件末尾、scss中嵌套尾换行
- ID、变量、函数、placeholder使用驼峰命名
- 颜色使用小写字母尽量用简写
- marign padding使用简写 font background transition animation尽量按顺序分开写
- @import不用`_`和`.sccc`后缀
- 嵌套层数不过5

### JavsScript(这块与<<javaScript语言精粹>>中提到的书写规范差不多)
也可以看[airbnb javascript的规范](https://github.com/airbnb/javascript)

- 运算符前后空格,`i++` `++i` `b: 1` 这种除外
- 变量声明,注释块,文件最后空行
- 属性声明`b: 1,` `{`, `else` `catch`, `finally` 变量赋值后换行
- 文档注释参考[usejsdoc](http://usejsdoc.org/)和[JSDoc Guide](http://yuri4ever.github.io/jsdoc/)
- 外层使用 `'` 单引号
- 函数变量都用驼峰式命名,特殊 ID,URL,Android,iOS JQuery对象变量以$开头
- 数组对象最后不要有逗号,对象属性名不加`'`