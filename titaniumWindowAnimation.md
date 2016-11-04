title: titanium给windows打开添加动画
date: 2016-03-06
tags: 
    - titanium
categories: 编程

---

在controller中打开一个新的页面一般都要调用：

```
Alloy.createController('index').getView().open()
```
<!-- more -->
可以将其拆分为(有点像jQuery的链式操作)：

```
controller = Alloy.createController('index')
top_view_is_default_window = controller.getView()
top_view_is_default_window.open()
```
可以衍生出窗口之间的动画切换功能:

```coffeeScript
//先拿到最顶层的window,默认为window,如果最顶层的视图不是alloy < window 则无法通过open()这种方法打开
top_view_is_default_window = Alloy.createController("index").getView()
//再将window整体向左边移动100%
top_view_is_default_window.setLeft("100%")
//再定义一个动画从左到右滑动的动画,可以方法可以全局，可以封装
slide_to_right = Titanium.UI.createAnimation()
slide_to_right.setLeft("100%").setRight("-100%").setDuration(200)
//在open的时候传入动画
top_view_is_default_window.open(slide_to_right)
```