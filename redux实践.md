title: redux实践
date: 2016-10-30
tags: 
    - redux
    - javascript
categories: 编程

---

redux是在看react时用于管理状态(state)，之前一直[发音](http://dict.cn/redux)错了(美[riː'dʌks]) 。

关于redux + react的[例子](https://github.com/lewis617/react-redux-tutorial)有很多，很多都是结合react来讲，react-redux中的connect, Provider方便了与redux之间的联系。

本篇文章中主要提到单纯的去使用和理解[redux](http://cn.redux.js.org//docs)

<!--more-->

需要额外准备的内容:

es6: 箭头函数, 属性的简洁表示法 

### 简介

#### redux中有几个常见的名词

action: 一种动作，能够用于修改store数据的唯一来源。一般通过store.dispatch()将action传递到store
reducer: 用于更新state同时返回一个新的state
store: 将action和reducer联系在一起,并维持state


#### store中有几个常用的方法

getState() : 获取store中的state
dispatch(action): 更新state
subscribe(listener): 注册和注销监听（返回函数注销监听） 

redux是单向的操作


action -> reducer -> state -> 

action -> reducer -> state ->

为了确保每次同一个action所改变的内容都一样，所以reducer函数里面的内容应该是一个纯函数(详细参考[FP](https://github.com/MostlyAdequate/mostly-adequate-guide),这个函数只处理state并返回一个新的state)

### action

现在我们手写一个action和一个action创建函数

```javascript
const ADD = 'ADD';

//action
{
  type: ADD,
  text: 'Build my first Redux app'
}
// action 创建函数

let add = (text) => {
    return {
        type: ADD,
        text
    };
}

```

看起来很简单是吧，action和action创建函数的区别在于有一个可复用的返回action的方法。

### redux

reducer是一个单纯的函数,只要传入参数相同，返回计算得到的下一个 state 就一定相同。

没有不同的返回值、不改变变量，仅仅只是计算, 如:

```javascript
let add3 = (num) =>  num + 3;

```


```javascript
const ADD = 'ADD';
const SUB = 'SUB';

const initState = {
    "add": 0,
    "sub": 0
};

let reducerSimple = (state = initState, action) => {
    switch (action.type) {
        case ADD:
            return Object.assign({}, state, {add: 1});
        case SUB:
            return Object.assign({}, state, {sub: 1});
        default:
            return Object.assign({}, state, initState);
    }
};
```

reducerSimple函数所执行的内容是获取action中的type参数并没有修改state的同时返回一个对应的,新的state。

### store

store就是用来处理action和reducer, 并注册事件监听和使用dispatch来更新state

```javascript
let store = createStore(reducerSimple);

store.subscribe(() => console.log(store.getState()));

store.dispatch(add('I am add'));
store.dispatch(add('I am sub'));
```

完整代码如下:

```javascript
import { createStore } from 'redux';

// public var
const ADD = 'ADD';
const SUB = 'SUB'

// action 
let add = (text) => {
    return {
        type: ADD,
        text
    };
};
let sub = (text) => {
    return {
        type: SUB,
        text
    };
};

// reducer
const initState = {
    "add": 0,
    "sub": 0
};

let reducerSimple = (state = initState, action) => {
    switch (action.type) {
        case ADD:
            return Object.assign({}, state, {add: 1, sub: 0});
        case SUB:
            return Object.assign({}, state, {add: 0, sub: 1});
        default:
            return Object.assign({}, state, initState);
    }
};

// store
let store = createStore(reducerSimple);

store.subscribe(() => console.log(store.getState()));

store.dispatch(add('I am add')); //{ add: 1, sub: 0 }
store.dispatch(sub('I am sub')); //{ add: 0, sub: 1 }
```

### 其他

继续值得优化的地方:

- 将action, reducer, store, public var, ... 分别放在不同的文件夹(actions,reducers,store,constnts),通过es6中module将不同的模块拆分
- 使用`combineReducers`合并不同的reducer
- 使用`Middleware`封装log记录

还有更高级的功能去探索:

- 异步action
- 异步数据流

我个人觉得不是所有的项目都需要用到redux，开发过程某一项工具类或者框架的使用应该慎重考虑，在需要用到的地方使用才能发挥出最大的威力。