title: js中的构造函数的继承
date: 2016-07-12
tags: 
    - javascript
categories: 编程

---

看了遍ruanyifeng老师写的[构造函数的继承](http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_inheritance.html),感觉刚认识javascript。下面的内容以烂笔头记录为主，重新写了下加深记忆，移步链接里面文章写的更详细。

<!--more-->  

js中对于构造函数的继承则有多种方式,因此能够共用公共的属性，减少重复代码的使用。

```javascript
function People(){
    this.species = "人类"
}

function PeopleFactory(name,gender){
    this.name = name,
    this.gender = gender
}
```

### 构造函数绑定

使用apply或call方法，将父类的构造函数绑定在子类对象上面。

```javascript
function PeopleFactory(name,gender){
    People.apply(this,arguments);  // or People.call(this,name,gender);
    this.name = name,
    this.gender = gender
}
var xiaoming = new PeopleFactory("xiaoMing","male");

console.log(xiaoming.species); //"人类"

```

### prototype模式

```
console.info(PeopleFactory.prototype.constructor == PeopleFactory); //true
PeopleFactory.prototype = new People();
console.log(PeopleFactory.prototype.constructor == People); //true
PeopleFactory.prototype.constructor = PeopleFactory;
console.info(PeopleFactory.prototype.constructor == PeopleFactory); //true

var xiaoming = new PeopleFactory("xiaoMing","male");
console.log(xiaoming.species); //"人类"
console.log(xiaoming.constructor == PeopleFactory.prototype.constructor); //true
```

构造函数的prototype发生变化时，它的prototype.constructor属性也会发生变化。实例对象的constructor属性等于构造函数的prototype.constructor属性。使用prototype模式继承构造函数时需要将继承链的constructor重新纠正成本身。

### 直接继承

利用不变属性prototype的方式，跳过使用new People()出的实例对象经行继承。改写People构造函数:

```
function People(){};
People.prototype.species = "人类";

PeopleFactory.prototype = People.prototype;
PeopleFactory.prototype.constructor = PeopleFactory;

var xiaoming = new PeopleFactory("xiaoMing","male");
console.log(xiaoming.species); //"人类"

```

这种方式的缺点是PeopleFactory和People共用一个prototype对象，PeopleFactory中改变了，则People也改变了。并且People.peprototype.constructor = peopleFactory。

### 利用空对象作为中介

由于第三种方法有缺陷，则有现这种方法。

```
var F = function(){};
F.prototype = People.prototype;
PeopleFactory.prototype = new F();
PeopleFactory.prototype.constructor = PeopleFactory;
```

封装之后变成
```
function extend(Child, Parent) {
　　var F = function(){};
　　F.prototype = Parent.prototype;
　　Child.prototype = new F();
　　Child.prototype.constructor = Child;
　　Child.uber = Parent.prototype; //这个属性直接指向父类的prototype,设置的uber属性是继承完备性
}

extend(PeopleFactory,People);
var xiaoming = new PeopleFactory("xiaoMing","male");
console.log(xiaoming.species); //"人类"
```

### 拷贝继承

将父类中的不变属性(prototype)拷贝到子类中来实现继承。

```
function extend2(Child, Parent) {
　　var p = Parent.prototype;
　　var c = Child.prototype;
　　for (var i in p) {
　　　　c[i] = p[i];
　　}
　　c.uber = p;
}
extend2(PeopleFactory,People);
var xiaoming = new PeopleFactory("xiaoMing","male");
console.log(xiaoming.species); //"人类"
```