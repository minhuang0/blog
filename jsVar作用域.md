title: var的作用域
date: 2015-12-15
tags: 
    - javascript
categories: 编程

---

变量的作用域分为全局变量和局部变量

js的变量的访问方式是内部函数可以访问外部或全局(不加`var`声明的也算)的变量,而外部不能访问内部函数的变量

在<<你不知道的JavaScript>>中第一章就详细讲解了作用域的概念。

<!--more-->  

### 变量寻值方式

下面的例子[引用](https://github.com/alsotang/node-lessons/tree/master/lesson11)则有说明到js中变量的寻值方式:

```javascript
//第三点: 假设此时外部定义了 childAge
//var childAge = '18';
var parent = function () {
  var name = "parent_name";
  var age = 13;

  var child = function () {
    var name = "child_name";
    var childAge = 0.3;

    // => child_name 13 0.3
    console.log(name, age, childAge);
  };

  child();

  // will throw Error
  // ReferenceError: childAge is not defined
  console.log(name, age, childAge);
};

parent();
```

第一次`console.log`时,会默认先去寻找`child function`中的name对象,找到了则打印,age在本方法中未定义,所以在`child function`的上下文中查找age变量。

第二次console中也是默认寻找`parent`中的`name`变量,此时`childAge`在`parent`中并没有定义,而是在`child function`中定义,js查找`parent function`中没有定义,联系上下文也没有定义,所以此时报错`childAge`没有定义

第三点: 假设我们把第二行代码取消注释，则此时的打印纪录是:

```console
child_name 13 0.3
parent_name 13 18
```

js查找上下文寻找变量的时候不会自己子方法中去查找,在本方中查询不到则回去外部作用域中去查找。

### 变量提升

如下例子，`var1`变量在`fun1`函数里面，由于并没有`var`什么，此时的`var1`实际上已经变量提升了，此时`var1`的变量也就变成了全局作用域。

```
function fun1(){
  var1 = 1;
}
```

