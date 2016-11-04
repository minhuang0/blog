title: NgShow And NgIf
date: 2016-03-06
tags: 
    - angular
categories: 编程

---

NgShow,NgIf用于使用变量来控制HTML块是否显示。与NgShow对应还有NgHide。

NgShow,NgHide所做的事情是控制`ng-hide`这个class,从语义上分析也是当`NgShow = false`和`ngHide = true` 时添加`ng-hide`class,反之则删除对应的`ng-hide`。

ng的渲染是在html DOM渲染之后，所以在使用ng-show的DOM页面开始存在而后又消失这种情况，可以在DOM上加上'ng-hide' class来手动默认隐藏状态。

NgIf则是值为true的情况才会渲染DOM元素,为false的情况下会删除DOM元素,并不是单纯的隐藏。

下面是测试当`ng-show = false`的DOM下Img的宽度是否产生变化，结果是不变。

```
<!DOCTYPE html>
    <html>
    <script src="http://ajax.googleapis.com/ajax/libs/angularjs/1.4.8/angular.min.js"></script>
    <body ng-app="">
        Show HTML: <input type="checkbox" ng-model="myVar">
        <button onClick="getImageWidth()">查看ng-show下面的图片宽度</button>
        <div ng-show="myVar">
            <h1>Welcome</h1>
            <p>Welcome to my home.</p>
            <img src="http://www.w3schools.com/tags/smiley.gif" id="img"></img>
        </div>
    </body>
    <script>
    function getImageWidth(){
        var img = document.getElementById('img');
        alert(img.width);
    }
    </script>
</html>
```