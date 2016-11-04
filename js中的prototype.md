title: js中的prototype(原型)
date: 2016-07-12
tags: 
    - javascript
categories: 编程

---

参考资料
 [ruanyifeng Javascript继承机制的设计思想](http://www.ruanyifeng.com/blog/2011/06/designing_ideas_of_inheritance_mechanism_in_javascript.html)

### prototype的由来

javascript设计之初是使用c++ 和 java中的new运算符来对构造函数进行实例对象,但new运算符的缺点,无法共享属性和方法，每一个实例对象都有自己的属性和方法,无法做到数据共享。

所以就引入了prototype属性,这个属性包含一个对象(prototype对象),所有实例对象需要共享的属性和方法，都放在这个对象里面；那些不需要共享的属性和方法，就放在构造函数里面。

实例对象被创建的时候会引用prototype的属性和方法。所有的实例对象共同享用prototype对象，好像是所有的实例对象"继承"了prototype对象。

<!--more-->  

### prototype的继承

使用prototype中的继承能够有减少重复属性或方法，所有实例对象指向同一个 prototype对象，减少内存地址的使用和提高运行效率。(例子来源于阮老师的文章)

```javascript
function Cat(name,color){
　　this.name = name;
　　this.color = color;
}

Cat.prototype.type = "猫科动物";
Cat.prototype.eat = function(){alert("吃老鼠")};
```
 
上面代码中每一个Cat的实例对象本地属性是name,color,而type,eat则是共享的，继承自prototype对象的属性。

```javascript
var cat1 = new Cat("大毛","黄色");
var cat2 = new Cat("二毛","黑色");
alert(cat1.type); // 猫科动物
cat1.eat(); // 吃老鼠
```

### prototype的验证方法

isPrototypeOf(): 用来判断prototype对象与实例的关系。
hasOwnProperty(): 判断是本地属性(true)和继承属性(false)
in:  运算符来判断是否有这个属性，无论本地属性和继承属性。

如果使用了prototype,在for..in语句中,会将prototype对象输出。可以使用hasOwnProperty判断是否是本地属性再输出则可以避免将prototype对象输出的情况。

```javascript
Array.prototype.testArg = "test";
var arr = [1,2,3,4];
for(array in arr){
    console.log(array);
}
// 0 1 2 3 testArg
for(array in arr){
    if(arr.hasOwnProperty(array)){
        console.log(array);
    }
}
// 0 1 2 3
```


