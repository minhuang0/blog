title: 读<<精通css第二版>>笔记
date: 2016-08-10
tags: 
    - css
categories: 编程

---
本篇内容：
    将自己在读这本书时自己不清楚或不知道的内容记录下来.
    
<!--more-->  

## 第二章: 为样式找到应用目标

元素选择器 ID选择器 Class选择器 通用选择器
### 伪类选择器 

链接伪类:link :visited,用于锚元素
动态伪类 :active :hover :focus
 IE6 应用于锚链接的:active和:hover选择器 忽略:focus,
 IE7 任何元素支持:hover,忽略 :active :focus

// 例子: 已访问链接和未访问链接鼠标悬停效果
```
a:visited:hover{color: olive}
```

### 高级选择器

子选择器,如 `ul > li`
IE7和高于其版本的都支持,在父类和子类之间有注释会产生BUG
IE6可以通过通用选择器模拟子选择器效果

相邻元素选择器, 如 `h2 + p`,指h2并列的第一个p标签

属性选择器,IE7及其以上支持
p[title]
p[title]:hover

IE6不支持属性选择器
可以通过下面的方式设置两种不通浏览器的风格

```
#header{
    background: url(branding_bw.png) repeat-y left top;
}
[id="header"]{
    background: url(branding_color.png)  repeat-y left top;
}
```

层叠

- 标有!important的用户样式
- 标有!important的作者样式
- 作者样式
- 用户样式
- 浏览器/用户代理应用的样式


选择器优先级,特殊性

| 选择器  | 特殊性(a,b,c,d)   | 以10为基数的特殊性  |
 ---- | ---- | ----
| Style="" | 1,0,0,0 | 1000 |
| #wrapper #content{} | 0,2,0,0 | 200 |
| #content .datePosted{} | 0,1,1,0 | 110 |
| div#content | 0,1,0,1 | 101 |
| #content | 0,1,0,0 | 100 |
| p.comment .dateposted{} | 0,0,2,1 | 21 |
| p.comment{} | 0,0,1,1 | 11 |
| div p{} | 0,0,0,2 | 2 |
| p{} | 0,0,0,1 | 1 |

- a = 行内样式
- b = ID选择器总数
- c = 类，伪类，属性选择器的总数
- d = 类型选择器和伪类选择器的数量

文档样式分割，但下面这种方式导入样式比链接样式表慢，影响下载时间，而且老式浏览器对于同时传输的文件数量有要求，所以更倾向于单一样式表而不是多个小文件。

```
/* css文件间可以使用import导入其他样式表 */
@import url(/css/layout.css)
```

在单一样式表中分割可以使用下面的注释来区分不同的模块

```
/* @group typography */
```

这样通过搜索`@group typ`就能够快速的定位了

样式文本结构如下:

- 一般性样式 `* @group gemeral styles`
    - 主体样式
    - reset样式
    - 链接
    - 标题
    - 其他元素
- 辅助样式 `@group helper styles`
    - 表单
    - 通知和错误
    - 一致的条目
- 页面结构 `@group page structure`
    - 标题，页脚，导航
    - 布局
    - 其他页面结构
- 页面组件 `@group page components`
    - 各个页面
- 覆盖 ``@group overrides

@todo 需要修改，复查的代码
@bugfix 表示代码或特定浏览器遇到的问题
@workaround 不完善的权益之计

### 第三章 可视化格式模型

box-sizing: 
标准盒模型(border-box): 内容区域width + 内边距width + 外边距width = width
IE非标准盒模型(content-box): width = 外边距width + 内边距width + 剩余的width(内容区域)
差异是标准盒模型由content,pandding,margin决定width,非标准盒模型固定width而压缩content

inline-block:   让元素能够像行内（inline）元素一样排列，内容符合块级框（block）的行为，能够设置高度，宽度,垂直外边距

block: 
垂直排列，垂直距离由verticle margin计算（重叠外边距）

position

relative: 占据原来位置和空间，发生偏移时会覆盖别的框
absoulte: 不占据空间，相对于距离它最近已定位的祖先元素而定位
fixed: 固定定位是绝对定位的一种,IE6不支持,IE7部分支持,实现会有些BUG
浮动:  浮动框向左右移动直到碰到包含框或者碰到另一个浮动的边缘，高度不一样时会卡住。
    清除浮动(下面的方法不适用于IE6):
        ```
        .clear:after{
            content: '';
            height: 0;
            visibility: hidden;
            display: block;
            clear: both;
        }
        ```

### 第四章 背景图像效果

#### 背景图

垂直渐变

```
body{
    background: #ccc url(img/gradient.png) repeat-x; //为了更贴近gradient.png最终的渐变色使背景无重叠
}
```

css圆角边框
 - 插入四张不同背景图在四个不同的标签上
 - 山顶角(图片变成透明的只遮住部分直角地方),由background-color控制边角颜色
css3圆角边框
 - 在一个标签上使用四张背景图,每张的图片,background-position,background-repeat用`,`分隔
 - border-radius 属性
 - border-image ,九分法缩放
   ```
   .box{
        -webkit-border-image: url(img/corners.gif) 25% 25% 25% 25% / 25px round round;
   }
   ```

#### 投影

简单投影
```
.img-wrapper{
    background: url(img/shadow.git) no-repeat bottom right;
    clear: right;
    float: left;
    position: relative;  /* 兼容IE6 */
}
.img-wrapper img{
    margin: -5px 5px 5px -5px;
    display: block; /* 兼容IE6 */
    position: relative;   /* 兼容IE6 */
}
/* 第二种方式 */
.img-wrapper img2{
    position: relative;
    left: -5px;
    top: -5px;
    
}
/* 使用css3 box-shadow属性 */
img{
    box-shadow: 3px 3px 6px #666;
}
```

透明度

使用opactiy后改元素的子类元素也继承这个属性
RGBa,a值的是alpha透明度这种情况下能够透明
png文件格式能够支持alpha透明度,IE6不支持,可以添加过滤器让它支持
```
div{
    filter:progid:DXImageTransform.Microsoft.AlpahImageLoader(src='/img/my-image.png',sizingMethod='crop');
    background: none;
}
```

### 第七章

border-spacing可以控制单元格之间的距离，IE7及以下版本不支持,可以使用cellspcing属性

label与input关联

隐式方式 
```
<label><input></input></label>
```
显式方式 

```
<label></label><input></input>
```

label for 对于input的ID，input name对应表单提交的key

fieldset用来分割不同的表单块
legend位于fieldset里面

```
<fieldset>
    <legend>title or explanatory caption</legend>
    <div>
        <label><label>
        <input></input>
    </div>
</fieldset>
```

注意: 

input[type='text'] 属性选择器不能再IE6及其以下版本使用

在编写表单的时候 :focus伪类选择器用在input,textarea上面能够提高用户体验

强调label的重要性可以在里面加入em,strong标签，将label 后面的input对齐可以

```
label{
    float: left;
    width: 10rem;
    cursor: pointer;
}
```

### 读完评价

看完了整本书，有些在电脑上看的，有的在地铁上手机看的。陆陆续续收获不少，解决了我一些不太清晰的地方，也对一些属性或名词有更深刻的理解（如position, float）,对于这块地方还查阅了别人的博客来交叉理解。

这是一本好的"API"，也是一本好的入门教材，以后遇到一些类似的问题还要来翻一翻。