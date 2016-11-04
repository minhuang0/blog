title: 封装html中的code
date: 2016-01-28
tags: 
    - javascript
    - html
categories: 编程

---
  
## 封装部分的html code重复使用: 
<!--more-->

### [load](http://api.jquery.com/load/)

```html
<!doctype html>
<head>
  <meta charset="utf-8">
  <title>load demo</title>
  <script src="https://code.jquery.com/jquery-1.10.2.js"></script>
</head>
<body>
 
<div id="testLoad"></div>
 
<script>
$("#testLoad").load("/resources/load.html");
</script>
 
</body>
</html>
```

### [imports](http://www.html5rocks.com/zh/tutorials/webcomponents/imports/)

warnings.html:

```html
<div class="warning">
  <style scoped>
    h3 {
      color: red;
    }
  </style>
  <h3>Warning!</h3>
  <p>This page is under construction</p>
</div>

<div class="outdated">
  <h3>Heads up!</h3>
  <p>This content may be out of date</p>
</div>
```

在index.html中复制一部分waring代码过来: 

```html
<head>
  <link rel="import" href="warnings.html">
</head>
<body>
  <script>
    var link = document.querySelector('link[rel="import"]');
    var content = link.import;

    // 从 warning.html 的文档中获取 DOM。
    var el = content.querySelector('.warning');

    document.body.appendChild(el.cloneNode(true));
  </script>
</body>
```

### [react](http://stackoverflow.com/questions/22461129/switch-class-on-tabs-with-react-js)写一个模块

下面是我写的一个例子: 
```
var React = require('react');

var TabComponent = React.createClass({
    getInitialState: function() {
        return {
            activeMenuItemTitle: 'Home'
        };
    },
    setActiveMenuItem: function(title) {
        this.setState({
            activeMenuItemTitle: title
        });
    },
    render: function() {
        var menuItems = this.props.data.map(function(menuItem) {
            return (
                <MenuItem active={this.state.activeMenuItemTitle === menuItem.title} key= {menuItem.title} onSelect= {this.setActiveMenuItem} title= {menuItem.title} href={menuItem.href}/>
            );
        }.bind(this));
        return (
            <ul className="nav nav-tabs" >
                {menuItems}
            </ul>
        );
    }
});

var MenuItem = React.createClass({
    handleClick: function(event) {
        //event.preventDefault();
        this.props.onSelect(this.props.title);
    },
    render: function() {
        var className = this.props.active ? 'active' : "";
        return (
            <li className={className} >
                <a href={this.props.href} onClick={this.handleClick} >{this.props.title}</a>
            </li>
        );
    }
});

module.exports = TabComponent;
```




