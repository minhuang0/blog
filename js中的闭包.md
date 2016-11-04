title: js中闭包的理解
date: 2016-07-15
tags: 
    - javascript
categories: 编程

---

***闭包的作用是让js能够从外部函数可以访问定义在内部函数中的变量,并且能够让这些值存在内存当中并进行读取、修改***

可以把闭包理解为定义在函数（fatherFunction）内部的子函数(childFunction)，我们可以通过这个方法来访问该方法fatherFunction中的局部变量

<!--more-->  

下面的例子则是利用闭包来做出函数式编程的例子。
预先把我们需要的值存进去，再通过返回的匿名function来访问预先存的值并进行运算。


```javascript
var adder = function (x) {
  var base = x;
  return function (n) {
    return n + base;
  };
};

var add10 = adder(10);
console.log(add10(5));
// => 15

var add20 = adder(20);
console.log(add20(5));
// => 25
```

上面的例子就是在 第三行 function中 `return n + base`此时在外面拿到返回方法的引用后,再次调用时。
此时的`base`则是引用了外部变量（虽然它们都在`adder function`里面）。


下面的例子看起来我们期望的是打印`0,1,2,3,4`,而实际打印的输出为`5,5,5,5,5`。

通俗的来说就是`setTimeout`方法是异步的，当5秒后打印i,而此时i的值经过循环已经变成了`5`。

```javascript
for (var i = 0; i < 5; i++) {
  setTimeout(function () {
    console.log(i);
  }, 5000);
}
```

这与我们预期的结果不同，由于没法保存i在每个循环的值，所以这时候我们可以用到闭包来做这个问题。

```javascript
for (var i = 0; i < 5; i++) {
  (function (idx) {
    setTimeout(function () {
      console.log(idx);
    }, 5000);
  })(i);
}
```

我们在for里面定义了一个立即执行的匿名函数

```
(function(idx){

})(i)
```

将`i`的值当做参数传递给这个函数,此时`console.log`打印idx则会访问到这个匿名函数里面的idx,此时由于后面的`console.log(idx)`还在使用`idx`,所以`idx`并还存在内存当中并没有被内存回收,这时候则会按我们的期望输出 `0,1,2,3,4`。

注意的是闭包会占用内存，所以不要滥用闭包，在适当的时候可以删除闭包里面的参数。