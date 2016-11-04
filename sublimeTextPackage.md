title: 配置sublime Text
date: 2016-04-01
tags: 
  - sublime-text
categories: 编程

---

- 安装package control, [链接](https://packagecontrol.io/installation)
	- 使用方式: 
		- ctrl + shift + p打开packge control的命令搜索栏
		- package install ,packge remove ,package list分别对应安装，移除，列表的功能
		- (步骤一)如选择package install 之后可以搜索自己喜欢的插件安装即可
        
<!-- more -->

- 接下来的其他插件可以选自己所需要的，或者在[流行](https://packagecontrol.io/browse/popular)插件里面选择
- emmet: 选择安装emmet包之后,使用方法在windows(ctrl + e)和mac(tab)上有区别
- 使用vim模式,注释掉 Preferences -> Setting - User文件里面 `"Vintage"`这行
- Soda Theme: 
	- 执行步骤一安装 theme-Soda
	- 打开Settings - User配置文件 在末尾追加 "theme": "Soda Light 3.sublime-theme", 可参见官方的文档` 
	- 保存之后还需要替换`color theme`,将下载下来的`theme`包(Espresso Soda.tmTheme,Monokai Soda.tmTheme)放在*Packages/User/*下
	- 在Preferences -> Color Scheme -> User这里设置一下对应的color theme
