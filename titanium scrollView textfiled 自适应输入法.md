title: titanium scrollView textfiled 自适应输入法(IOS)
date: 2015-03-16
tags: 
    - titanium

categories: 编程

---

[参考文档](https://github.com/appcelerator/titanium_mobile/blob/master/demos/KitchenSink/Resources/examples/textfield_scrollview.js)
<!-- more -->
安卓上面能够自动上移,在IOS能够自适应输入法：

核心代码为：
ScrollView(contentWidth='auto' contentHeight='auto' showVerticalScrollIndicator='true' showHorizontalScrollIndicator='false' top=0 borderColor='red')

1.需要一个scrollview包裹着textfield

2.scrollview里面的功能是为了适应TextField的多样式，里面可以写很多不同的控件，

3.包裹scrollview的外部view或者window不能有layou 是vertical 或者 horizontal