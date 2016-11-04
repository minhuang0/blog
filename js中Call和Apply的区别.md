title: js中Call()和Apply()的区别
date: 2016-07-12
tags: 
    - javascript
categories: 编程

---

### 差异

相同点: call和apply都是改变函数的作用域(改变函数的上下文),改变函数作用域中this的指向。通俗来讲就是调用别的对象，当做自己的方法来使用。
区别: 两者传递的参数不一样。call用于明确参数个数时使用，apply可以用来不明确参数个数时使用。

参数区别: 两者的第一个参数都是指针的指向对象。call的有多个参数，而foo的参数是两个，后者为一个参数数组。

<!--more-->  

下面是foo,call使用foo这个方法的表达式，也表明了两者之间的关系:

```javascript
foo.call(this, arg1,arg2,arg3) == foo.apply(this, arguments)==this.foo(arg1, arg2, arg3)
```

其中arguments对象是实参个数决定的一个非Array示例的数组,如下例子:

```javascript  

Array.prototype.testArg = "test";
function testArguments(a,b,c){
    console.log(arguments);
    console.log(arguments.testArg);
}

testArguments('a','b'); //["a", "b"] undefined
```

### 例子

下面是一个使用apply和call的例子

```
function foo(){
    console.log(this.name);
}
function foo2(gender,age){
    console.info(this.name + " is " + gender + " and " + age);
}

var name = "Jack";
var hero = {
    name : "Nike"
};

foo(); //Jack
foo.apply(window); //Jack
foo.apply(hero);  //Nike
foo.call(hero); //Nike

foo2('male',18); //Jack is male and 18
foo2.apply(window,['male',18]); //Jack is male and 18
foo2.apply(hero,['male',18]); //Nike is male and 18
foo2.call(hero,'female',18); //Nike is female and 18

```

通将foo2绑定到apply 或 call 第一个参数(对象)上面, 在这个对象上面增加了foo2这个方法。