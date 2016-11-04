title: 读ECMAScript 6记录
date: 2016-03-06
tags: 
    - javascript
    - ES6
categories: 编程

---
记录一些学习过程中的收获,[文档地址](http://es6.ruanyifeng.com/)

<!--more-->  

### let 不变量提升,不能重复声明,对当前作用域起作用,暂时性死区

let和var不同的一点是let不会变量提升,只作用于当前作用域(块级作用域)

```
var tmp = "myTmp";
if (true) {
    console.log(tmp); // ReferenceError   //TDZ(temporal dead zone -> '暂时性死区')开始
    let tmp = 'tmp';   //TDZ结束，在
}
```

暂时性死区的本质是为了防止在变量声明前就使用该变量,只有等到声明后才可以使用

arg默认被声明了,此时不能重复声明arg
```
function func(arg){
	let arg; //报错
}
```

有个非常有趣的例子: 

```
var a = [];
for (var i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i);
  };
}
a[6](); // 10
```

```
var a = [];
for (let i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i);
  };
}
a[6](); // 6
```

使用let只在当前作用域生效,而var在全局范围都有效,所以此时输出是i的值为10。

### 作用域: 全局作用域,函数作用域,块级作用域

```
{
    console.info("块级作用域");
}
```

块级作用域避免内层变量对全局变量的改写和泄漏导致全局新增变量

块级作用域能够让立即执行匿名函数（IIFE）不必须了

```
// IIFE写法
(function () {
  var tmp = ...;
  ...
}());

// 块级作用域写法
{
  let tmp = ...;
  ...
}
```

### const为常量,需要立即声明

const命令,对常量声明后不可改变;与let相同点:块级作用域,无变量提升,不可重复声明,存在暂时性死区


### ES6变量声明方法

- var
- function
- let
- const
- import
- class

let,const,class声明的全局变量，不属于全局对象(global,window)的属性

```
let b = 1;
window.b // undefined
```

node里面的全局变量是global,浏览器里面的是window

### 结构赋值

数组用[]按顺序结构,对象用{}，变量需要与属性同名才能取到正确值而不是undefined

解构赋值的内部机制，是先找到同名属性，然后再赋给对应的变量
```
var { bar, foo } = { foo: "aaa", bar: "bbb" }; // 等于下面的例子
var { foo: foo, bar: bar } = { foo: "aaa", bar: "bbb" };

```

解构:

```
let[x,,y] = [1,2,3];
x //1
y //3

var {bar,foo} = {foo: "aaa", bar: "bbb"};
foo // "aaa"
bar // "bbb"
```
用途:
交换变量值:

```
[x,y] = [y,x];
```
返回一个数组:

```
function example(){
	return [1,2,3];
}
var [a,b,c] = example();
```

提取JSON数组

参数默认值

for..of获取key and value

加载模块指定方法

```
const { SourceMapConsumer, SourceNode } = require("source-map");
```

### 数值的扩展

全局方法: parseInt() parseFloat()移植到Number对象上面。
**Number.parseInt**，**Number.parseFloat**，改变了8进制16进制的开头。

```
//ES5
parseInt("12.34") // 12
parseFloat("123.45#") //123.45

//ES6
Number.parseInt("12.34") //12
Number.parseFloat("123.45#") //123.45
```

`Number.isInteger()` 判断是否为整数

Math对象扩展

`Math.trunc()` 去小数 `Math.sign()`判断正数负数零 这两个应该常用.

更多在[w3c](http://www.w3schools.com/js/js_reserved.asp)查看

数组的扩展

`Array.from()` 将类似数组的对象和可遍历的对象变为真正的数组

```
let ps = document.querySelectorAll('p');
Array.from(ps).forEach(function(p){
	console.log(p);
})
```

可以接受第二个参数,下面的例子将数组中布尔值为false的成员转为0。

```
￼Array.from([1, , 2, , 3], (n) => n || 0) // [1, 0, 2, 0, 3]
```

`Array.of()` 将一组值转换为数组

```
Array.of(3, 11, 8) // [3,11,8] 
Array.of(3) // [3] 
Array.of(3).length // 1
```

对象的扩展

```
function f( x, y ) { 
	return { x, y };
}
// 等同于
function f( x, y ) { 
	return { x: x, y: y};
}
```

属性表达式 定义方法名,对象时使用

```
// 方法一 obj.foo = true;
// 方法二 obj['a'+'bc'] = 123;
```



Math增加cbrt立方根，hypot平方和开根号等方法

### 字符的扩展

Unicode表示法

`\uxxxx`,xxxx表示字符码点

这种表现形式适用于\u0000——\uFFFF之间的字符，`\u20BB7` 会被理解为 `\u20BB` + 7 = " 7",ES6中给码点增加{}即可,'\u{20BB7}'

codePointAt(idx): 将字符转换为10进制码点,idx是字符在字符串中的位置
String.fromCodePoint(): 是将一个或多个码点转化为字符

for ..of 能够遍历大于0xFFFF的码点. for会将大于0xFFFF的码点当做两个字符，都不可以打印出来

es5的charAt是返回UTF-16编码的第一个字节,不能被打印. at能够识别Unicode大于0xFFFF字符的第一个字节

es5中的indexof能够确定字符串是否包含在另一个字符串中

**includes**: 返回是字符串否包含该字符的布尔值,第二个参数指从当前位置到最后
startsWith: 返回是字符串开头是否包含该字符的布尔值,第二个参数指从当前位置到最后
endsWith: 返回是字符串结尾是否包含该字符的布尔值,第二个参数指从当前位置到最前的位置

repeat返回一个新的字符串,该字符重复n(参数)次

ES7增加了**padStart**,**padEnd**: 在头部或者尾部补齐指定长度的字符串(实用呀)

```javascript
'1'.padStart(10, '0') // "0000000001"
'12'.padStart(10, '0') // "0000000012"
'123456'.padStart(10, '0') // "0000123456"

'12'.padStart(10, 'YYYY-MM-DD') // "YYYY-MM-12"
'09-12'.padStart(10, 'YYYY-MM-DD') // "YYYY-09-12"
```

**[字符串模板](http://es6.ruanyifeng.com/#docs/string)**

实用反引号（```）标示,变量名要写在 `${}` 中,`${}`可以写表达式,引用,方法,嵌套,使用条件语句。如下所示:

```javascript
$('#result').append(`
  There are <b>${basket.count * 2 * getNum()}</b> items
   in your basket, <em>${basket.onSale}</em>
  are on sale!
`);
```


> 备注: es5中的[trim](https://msdn.microsoft.com/library/ff679971) 能够移除字符串中的已移除前导空格、尾随空格和行终止符的原始字符串
移除的字符包括空格、制表符、换页符、回车符和换行符

嵌套:

```javascript
const tmpl = addrs => `
  <table>
  ${addrs.map(addr => `
    <tr><td>${addr.first}</td></tr>
    <tr><td>${addr.last}</td></tr>
  `).join('')}
  </table>
`;
```

引用模板字符串本身，在需要时执行，可以像下面这样写。
```javascript
// 写法一
let str = 'return ' + '`Hello ${name}!`';
let func = new Function('name', str);
func('Jack') // "Hello Jack!"

// 写法二
let str = '(name) => `Hello ${name}!`';
let func = eval.call(null, str);
func('Jack') // "Hello Jack!"

```

模板的实例:

看着下面这段代码是不是特别熟悉,有种Rect JSX, Rails或者Node里面template的熟悉感觉。
```javascript
var template = `
<ul>
  <% for(var i=0; i < data.supplies.length; i++) { %>
    <li><%= data.supplies[i] %></li>
  <% } %>
</ul>
`;
```

思路做的是将字符串中`<% %>`JavaScript代码和`<%= %>`JavaScript表达式转换为表达式字符串,然后将拼接在一起。

```javascript
echo('<ul>');
for(var i=0; i < data.supplies.length; i++) {
  echo('<li>');
  echo(data.supplies[i]);
  echo('</li>');
};
echo('</ul>');
```

这段正则是用来匹配替换掉`<% %>`和`<%= %>`的,用来生成`echo('String')`组成的字符和能够直接执行的JavaScript代码,
因此在`compile`使用时要加上`eval`来执行里面的JavaScript代码

```javascript
function compile(template){
  var evalExpr = /<%=(.+?)%>/g;  
  var expr = /<%([\s\S]+?)%>/g;

  template = template
    .replace(evalExpr, '`); \n  echo( $1 ); \n  echo(`')
    .replace(expr, '`); \n $1 \n  echo(`');

  template = 'echo(`' + template + '`);';

  var script =
  `(function parse(data){
    var output = "";

    function echo(html){
      output += html;
    }

    ${ template }

    return output;
  })`;

  return script;
}
```


用法如下: 

```javascript
var parse = eval(compile(template));
div.innerHTML = parse({ supplies: [ "broom", "mop", "cleaner" ] });
//   <ul>
//     <li>broom</li>
//     <li>mop</li>
//     <li>cleaner</li>
//   </ul>
```

标签模板可用来过滤HTML字符串,多语言转换（国际化处理）

### 数组的扩展

Array.from: 将类似数组的对象(array-like object)和可遍历(iterable)的对象(包括ES6的Set和Map);

常用转换对象有 DOM操作里面的Nodelist集合(有`length`方法的),arguments对象,扩展运算符对象(`...`)

```javascript
Array.from(document.querySelectorAll('p')).forEach(function(p){
  console.log(p);
});
```

Array.of(num) 创建数组,num = 0时为`[]` ,为一个参数时创建num长度的数组
copyWithin复制数组内部的值

```javascript
Array.prototype.copyWithin(target, start = 0, end = this.length)
```
find 寻找数组里面符合条件的值并返回该值
findIndex返回数组内部第一个符合条件的位置,没有找到返回-1

弥补indexOf的不足

```javascript
[NaN].indexOf(NaN)
// -1

[NaN].findIndex(y => Object.is(NaN, y))
// 0
```

fill(value,start,end) 通过给定value值,填充数组,可选参数start end可以改变填充位置


entries() keys() values() 通过`for...of`能够对应遍历键值对,键名,键值

```javascript
for (let [index, elem] of ['a', 'b'].entries()) {
  console.log(index, elem);
}
// 0 "a"
// 1 "b"
```

includes() 搜索是否包含指定值

空位 

`[,1,,1]` ES6中统一规定空位的值为`undefined`

新增的数组方法都不忽略空位, for...of能够遍历出空位

### 函数的扩展

**函数的默认值**

在ES5中当函数的默认值一般都用`||`表达式,但在输入值为`false`的情况则就不能了，可以通过三元表达式来完成 `x === false ? true : false`

ES6设置函数的默认值是直接写在参数定义后面

```
function Point(x, y = 5){
  // let x = 1; //注意此时的x和y都不能用let,const再次声明
  // 这种情况下能够很清晰的就知道y是不必须写的,x必须传递
}
```

参数与解构赋值一起使用

箭头函数与变量解构结合使用

```javascript
const full = ({first, last}) => first + " " + last;

//等于
function full(person){
  return person.first + " " + person.last;
}
```

箭头函数的注意点:

- this是定义所在的对象,不是使用时所在对象
- 不可以做构造函数,使用new命令
- 不可以使用arguments对象
- 不可以使用yield对象

伪调用优化
伪调用递归

###　对象的扩展

属性简写: 

```
var birth = '2000/01/01';

var Person = {

  name: '张三',

  //等同于birth: birth
  birth,

  // 等同于hello: function ()...
  hello() { console.log('我的名字是', this.name); }

};
```

属性表达式

```
var lastWord = 'last word';

var a = {
  'first word': 'hello',
  [lastWord]: 'world'
};

a['first word'] // "hello"
a[lastWord] // "world"
a['last word'] // "world"
```

**属性表达式不能与简写表达式同时使用**

name属性

object.is比较两个值是否相等

object.assign(target ,source1, source2) 用于对象的合并,浅拷贝

添加属性和方法


### Symbol

7种数据类型: Undefind, Null, String, Number, Object, Boolean, Symbol

在处理单例的时候能够通过单例来是引用对象不被重写

```
// mod.js
const FOO_KEY = Symbol.for('foo');

function A() {
  this.foo = 'hello';
}

if (!global[FOO_KEY]) {
  global[FOO_KEY] = new A();
}

module.exports = global[FOO_KEY];
```

### Proxy 和 Reflect

### Set and  Map

Set类似于数组,但成员唯一 

```
function dedupe(array) {
  return Array.from(new Set(array));
}

dedupe([1, 1, 2, 3]) // [1, 2, 3]
```

WeakSet与Set的区别是只接受数组或者类似数组的对象作为参数,无Size属性，不能进行遍历

Map能存放对象，和内存地址绑定

```
var map = new Map();

var k1 = ['a'];
var k2 = ['a'];

map
.set(k1, 111)
.set(k2, 222);

map.get(k1) // 111
map.get(k2) // 222
```

看完之后在多个项目中使用过后才知道es6带来的一些实际方便，这本书不仅是一本入门教程，也是一本API，在不清楚或者忘记某个方法时需要多来翻一翻。