title: 对js中的数组理解
date: 2015-12-15
tags: 
    - javascript
categories: 编程

---

TODO: 重新理一遍数组

<!--more-->

平时用到了多次的数组，可数组本来结构是什么却不是很清楚。

```javascript
var numbers = ['zero', 'one', 'two', 'three', 'fore'] 
```

数组`numbers`第一个值获得属性名'0',第二个值获得属性名'1',所以能够通过numbers[0]取得zero的值
对象的字面量:

```javascript
var numbers_object = {
    '0':'zero',
    '1':'one',
    '2':'two',
    '3':'three',
    '4':'fore'
} 
```
numbers与nubmers_objext对比,numbers继承的array.prototype,numbers_object继承的object.prototype。所以numbers继承了很多方法。length属性是一个诡异的属性,length没有上界,不一定等于数组属性的个数。

```javascript
var myArray = [];
myArray.length //0
```
数组最后插入一条记录:

```
numbers.length  = 3; //numbers是['zero', 'one', 'two']
numbers[numbers.length] = 'three'; //nubers是['zero', 'one', 'two', 'three']
numbers.push('fore'); //numbers是['zero', 'one', 'two', 'three', 'fore']
```

