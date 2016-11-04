title: 更改checkbox radio的默认选中效果
date: 2016-06-23
tags: 
    - html
    - css
categories: 编程

---

将checkbox或者raido自定义在制作表单页面相关的时候经常能够用的到。
<!--more-->  
下面是一种自定义的方法:

如下HTML代码:

```html
<div class="radio-toolbar">  
    <input type="radio" id="radio1" name="radios" value="all" checked>
    <label for="radio1">All</label>
    <input type="radio" id="radio2" name="radios"value="false">
    <label for="radio2">Open</label>
    <input type="radio" id="radio3" name="radios" value="true">
    <label for="radio3">Archived</label>
</div>
```
这里的[label](http://www.w3school.com.cn/tags/tag_label.asp)中for属性指向了三个不同的id,指当点击label中的文本浏览器会自动将焦点转到和标签相关的表单控件上。作用是radio或checkbox增大点击范围。

CSS代码:

```css
.radio-toolbar input[type="radio"] {
    display:none;
}

.radio-toolbar label {
    padding-left: 20px; 
    background: url("no_checked.png") no-repeat 0 0/auto 100%;
}

.radio-toolbar input[type="radio"]:checked + label {
    background: url("checked.png") no-repeat 0 0 / auto 100%;
}
```
class 1 指的将`.radio-toolbar`下面的type为`radio`的input标签隐藏,不占用文档空间。
class 2 将label向右侧移动,并替换自己需要的默认不选中时的效果。
class 3 将所有紧邻(+为[相邻兄弟选择器](http://www.w3school.com.cn/css/css_selector_adjacent_sibling.asp))input(满足`type='raido'`并且被选中(checked))的label标签

checkbox使用方式雷同，将radio替换成checkbox。

刷新页面，则会看到自定义的radio,checkbox自定义样式

参考: 

[链接1](http://stackoverflow.com/questions/4641752/css-how-to-style-a-selected-radio-buttons-label)
[链接2](http://code.stephenmorley.org/html-and-css/styling-checkboxes-and-radio-buttons/)

