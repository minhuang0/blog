title: 实现浮动使用inline-block和float的区别
date: 2016-07-01
tags: 
    - html
categories: 编程

---

inline-block在盒子内部表现形式如block元素,例如可以改变width,height,padding,margin等属性。而在外部的表现形式像inline元素,从水平排列,例如`<span></span><span></span>` 这种排列形式会水平排列在一行。

关于这三者的区别可以看[链接](http://stackoverflow.com/questions/8969381/what-is-the-difference-between-display-inline-and-display-inline-block) or [这](http://www.cnblogs.com/jdonson/archive/2011/06/10/2077932.html)

inline-block与float都能够做到一些浮动的效果，但还是有一些区别:

float脱离文档流并让周边元素围绕这个元素，inline-block在文档流内，周围元素不会围绕它。

因此由于float脱离了文档流，不受父类text-algin: center的影响，而inline-block相反。 同样inline-block受verticle的影响，能够改变基线。

float会自动将空白节点忽略，让元素间没有空白。而inline-block相反,去除inline-block间的空白解决方式:

- 删除html中空白节点
- 使用margin: -xx边距
- font-size: 0


[参考链接](https://designshack.net/articles/css/whats-the-deal-with-display-inline-block/)
[参考链接](http://www.w3cplus.com/css/inline-blocks.html)
