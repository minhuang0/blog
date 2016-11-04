title: titanium手指控制图片缩放（IOS）
date: 2015-03-16
tags: 
    - titanium

categories: 编程

---

原理是用到了[imageview-zooming](https://developer.appcelerator.com/question/121257/imageview-zooming)个属性

<!-- more -->

分为三个步骤，也可以将1.2步全部写在coffee(现在回过头来整理coffee,jade真是太痛苦了)里面

- image_zoom.coffee 

```coffeeScript
args = arguments[0] || {}
image_view = Titanium.UI.createImageView(
    image: Settings.server + args  
    width: '100%'
    height: Ti.UI.SIZE
)
$.scrollView.add(image_view)
$.scrollView.addEventListener 'click',->
    $.image_zoom.close()                   
```    
- image_zoom.jade  

```jade
Alloy
    Window
        View(backgroundColor='black' layout='vertical' center='true')
            ScrollView#scrollView(width='100%' height='100%' showHorizontalScrollIndicator='false' showVerticalScrollIndicator='false' maxZoomScale='10' minZoomScale='1.0' backgroundColor="transparent" center='true')      
```
- other.coffee(调用图片缩放页面)  

```
Alloy.createController("image_zoom",remote_data.pic).getView().open()      
```