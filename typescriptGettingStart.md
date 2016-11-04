title: typescript getting start
date: 2016-03-06
tags: 
    - typescript
    - javascript

categories: 编程

---

> 文章中typescript中简写为ts

<!--more-->  

### 类型注解

```typescript
function setString(str: string){
    console.log(str);
}
```

params: type 这种方式能够在编译ts时给出error提示,但不影响编译成js文件

### 接口

```typescript
interface Person{
    firstName: string,
    lastName: string
}

function setName(person: Person){
    console.log(person.firstName + person.lastName);
}
```

能够通过接口定义参数的结构形状

### 类

类可以配合接口使用定义参数结构形状，类里面`contructor`的参数中`public params` 能够将该`params`能够简为该类简写属性
```typescript
class Student{
    fullName: string;
    constructor(public firstName, public middleInitial, public lastName){
        this.fullName = firstName + " " + middleInitial + " " + lastName;
    }
}
```
编译出来的javascript代码为:

```javascript
var Student = (function () {
    function Student(firstName, middleInitial, lastName) {
        this.firstName = firstName;
        this.middleInitial = middleInitial;
        this.lastName = lastName;
        this.fullName = firstName + " " + middleInitial + " " + lastName;
    }
    return Student;
}());
```

待续...