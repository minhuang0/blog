title: Sass使用笔记
date: 2016-05-10
tags: 
  - sass
  - web
categories: 编程

---

使用[Sass](http://sass-lang.com/documentation/file.SASS_REFERENCE.html)和前面提到的Sui-mobile的ui框架开发嵌入微信端的页面。
<!-- more -->

主要用到的功能: 

变量: 

```sass
$normal-color: #666666;

p{
	color: $normal-color;
}
```
嵌套: 
```sass
.header{
	.title{
		color: black;
	}
	&:hover{
		color: #ffffff;
	}
	/* 
	&代表.header, 编译出来: 
	.header:hover{
		color: #ffffff;
	} 
	*/
}
```
继承:

```sass
.public-normal-button{
	border-radius: 4px;
}
.button{
	@extend .public-normal-button;
	color: black;
}

```
@mixin:
```
　　@mixin left($value: 10px) {
　　　　position: absolute;
　　　　left: $value;
　　}
　　/* 此时10px为默认参数 */
　　div {
　　　　@include left(20px);
　　}
```
import:

```
@import "foo.css";
/* 引入当前页面的foo.css文件 */
```

还未用到的: 

```sass
@if @else @for @while 条件语句

@function test(){
}

运算

颜色计算

@media
```


命令:

安装: gem install sass
编译scss => css: sass input.scss output.css
监听文件改变并自动编译: sass --watch app/sass:public/stylesheets