title: ReactJs笔记
date: 2016-01-13
tags: 
    - react
    - javascript
categories: 编程

---

# [React](https://github.com/facebook/react)
<!--more-->  
将独立的UI用*JSX*(js和xml混合的语法)定义的方法将代码封装成组件,再由多个子控件组成页面。

JSX并不是React必须的

```
React.createElement('a', {href: 'http://facebook.github.io/react/'}, 'Hello React!')
```
等价于JSX语法:

```
<a href="http://facebook.github.io/react/">Hello React!</a>
```
看起来像XML的JavaScript语法扩展



`React.Reander`: 基本方法,用于将模版转化为HTML语音

HTML以`<`开头,JavaScript以代码块开头`{`

组件类: 由React.createClass生成的类,命名规则首字母大写,必需有个返回唯一顶层标签的`render`方法输入组件。

```
var HelloMessage = React.createClass({
  render: function() {
    return <h1>Hello {this.props.name}</h1>;
  }
});

ReactDOM.render(
  <HelloMessage name="John" />,
  document.getElementById('example')
);
```

> `<h1>`则为顶层标签, HelloMessage首字母为大写。

DOM （virtual DOM）虚拟的DOM,先变化成虚拟的DOM,然后再对应到真实的DOM。this.refs.[refName]能拿到在虚拟DOM里面定义了ref属性的对象。

this.props and this.state: 前者是父类过来不可变动的属性(只读的),后者指可以变化的属性,与用户交互的属性

State 应该包括那些可能被组件的事件处理器改变并触发用户界面更新的数据

React响应式更新概念是局部刷新,通过status的变化让Virtual DOM变化,再实现到真实的DOM上面。效率更高效

封装性、组件代码的复用性、测试和separation of concerns

> 不要低估 JavaScript 的速度，DOM 操作通常才是慢的原因。
