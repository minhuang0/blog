title: 图片不间断循环
date: 2016-06-09
tags: 
  - css
  - jquery
categories: 编程

---
需要做一个条纹上下不停运动的动画,或者路面水平不断的移动
<!--more-->  
解决方案

原理是将div包裹img,并将div的overflow设为hidden，并固定div的宽高。img的图片高度要大于div的高度,运动的时候改变图片的margin-top or marigin-left值。

下面是写的一个Class来实现这个方法,依赖jQuery。


```
function RollElement(elem, speed) {
    var self = this;
    this.elem = elem;
    var speed = 20 || speed;
    var width = parseInt(elem.css("width"));
    var height = parseInt(elem.css("height"));
    var img = elem.find("img");
    this.left = function() {
        var imgWidth = parseInt(img.css("width"));
        var offsetHorizon = imgWidth - width;
        img.animate({
            marginLeft: -offsetHorizon
        }, offsetHorizon * speed, "linear", function() {
            img.css("marginLeft", 0);
            self.left();
        });
    }
    this.right = function() {
        var imgWidth = parseInt(img.css("width"));
        var offsetHorizon = imgWidth - width;
        img.css("marginLeft", -offsetHorizon).animate({
            marginLeft: 0
        }, offsetHorizon * speed, "linear", function() {
            img.css("marginLeft", -offsetHorizon);
            self.right();
        });
    }
    this.up = function() {
        var imgHeight = parseInt(img.css("height"));
        var offsetVerticle = imgHeight - height;
        img.animate({
            marginTop: -offsetVerticle
        }, offsetVerticle * speed, "linear", function() {
            img.css("marginTop", 0);
            self.up();
        });
    }
    this.down = function() {
        var imgHeight = parseInt(img.css("height"));
        var offsetVerticle = imgHeight - height;
        img.css("marginTop", -offsetVerticle).animate({
            marginTop: 0
        }, offsetVerticle * speed, "linear", function() {
            img.css("marginTop", -offsetVerticle);
            self.down();
        });
    }
    this.stop = function() {
        img.stop().css({
            "marginLeft": 0,
            "marginTop": 0
        });
    }

    this.changeSpeed = function(newSpeed) {
        speed = newSpeed;
        img.css({
            "marginLeft": 0,
            "marginTop": 0
        });
    }
}
//使用方式
var road = new RollElement($(".road"));
road.left();
```
