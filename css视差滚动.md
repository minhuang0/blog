title: css视差滚动
date: 2016-07-25
tags: 
    - css
    - html
categories: 编程

---

看到<<精通css>>中背景图这一章节提到视差效果, 在一个背景区域叠加不同的背景图片,通过调整`background-position`的值,将三个不同的图片位置设置不同的百分比。当浏览器宽度发生变化时,三个背景图会以不一样的速度移动,从而产生'动态'的效果。

于是google下视差效果,出来了视差滚动。发现使用`background-attchment`这个属性能做出很棒的滚动效果([效果](https://codyhouse.co/demo/alternate-fixed-scroll-background/index.html))。

<!-- more -->

通过不同背景图的做的视差效果代码如下:
```
.bg {
    background-repeat: repeat-x;
    background-color: transparent;
    background-size: auto 100%;
    min-height: 200px;
}

.bg-1 {
    background-image: url('../images/4.png');
    background-position: 20% 0;
}

.bg-2 {
    background-image: url('../images/3.png');
    background-position: 40% 0;
}
```

当屏幕宽度变化的时候,两个背景图会以不同的速度进行偏移,类似于一种动态的效果。

通过css3的多背景图片可以简化上面的代码,将不同的背景图放在同一个class里面,通过设置不同的url和position达到同样的效果[demo](http://www.huangmin.me/demo/html/css视差效果.html)。

```
.bg {
    background-repeat: repeat-x;
    background-color: transparent;
    background-size: auto 100%;
    min-height: 200px
}

.bg-1 {
    background-image: url('../images/4.png'), url('../images/3.png');
    background-position: 20% 0, 40% 0;
}
```

下面是介绍视差滚动,w3cschool种关于[background-attachment](http://www.w3schools.com/cssref/pr_background-attachment.asp)的介绍,作用设置背景图像是否固定或者随着页面的其余部分滚动，当为fixed时则固定页面背景图片不随屏幕滚动而滚动。[demo](http://www.huangmin.me/demo/html/css视差滚动.html)

```
.fixed-bg{
    min-height: 100%;
    background-size: cover;
    background-attachment: fixed;
    background-repeat: no-repeat;
    background-position: center center;
}
.fixed-bg.fixed-bg-1{
    background-image: url(../images/1.png);
}
.fixed-bg.fixed-bg-2{
    background-image: url(../images/2.png);
}
.scrolling-bg{
    min-height: 100%;
    background-color: #001224;
}
```

background-attachment这个属性是不可少的，

```
background-attachment: fixed;
```
