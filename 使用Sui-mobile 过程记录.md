title: Sui-mobile使用心得
date: 2016-05-10
tags: 
  - sui-mobile
  - web
categories: 编程

---
 
链接: [Sui-mobile](https://github.com/sdc-alibaba/SUI-Mobile)
<!--more--> 
限于我用的时间2016/5/10时

优点: 

- 手机端双平台的适配做的很好
-  有写很常用的ui组件,如picker,日历,侧滑栏，菜单栏，搜索栏等

有待改善的地方:

- api文档不详细
- issues还有比较多的没有合适的解决方案。（ issues open 286/closed 299 ）例如: 
   - 在router这一块处理的不太好,在页面重复打开后退打开的情况下，会出现页面不能跳转的问题，后面的做法将全部的路由都关闭。
   - 一个页面存在多个datetimepicker的时候会产生bug

总体: 

总体还是很不错的，需要优化的地方有很多，在wechat上面快速的开发并嵌入一个web页面是个不错的选择