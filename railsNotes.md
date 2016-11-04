title: Rails笔记
date: 2015-09-23
tags: 
    - rails
categories: 编程

---

记录一些开发Rails中觉得有用的方法
<!--more--> 

- rails跨域请求
在 *config/application.rb* 中 `class Application < Rails::Application` `end`中间添加:     

```ruby
 config.action_dispatch.default_headers.merge!({
      'Access-Control-Allow-Origin' => '*',
      'Access-Control-Request-Method' => '*'
})
```

 

- 导航栏高亮
写导航栏的时候不知道该如何让选中的菜单高亮，每次都会选中初始的选择项

这两种方式是我借鉴的:
http://stackoverflow.com/questions/14248258/ruby-on-rails-website-adding-removing-active-class-to-navbar
http://stackoverflow.com/questions/17481812/dynamically-add-active-class-to-bootstrap-li-in-rails


原理就是写一个全局的方法，然后在html页面中调用这个方法，判断是否当前的页面是否是传参进去的页面值，从而给出是否给自己的标签添加一个高亮的类

第一种方法中的params[:action]也可以换成params[:controller]来判断,如下所示:

*app/helpers/application_helper.rb*

```ruby
module ApplicationHelper
  def hover_class(link_path)
    params[:controller] ==  link_path ? "hover" : ""
  end
end
```
*app/views/layout.application.html.erb*

```html
<li> <%= link_to "用户管理", users_path , class: hover_class('users')  %> </li>
```
