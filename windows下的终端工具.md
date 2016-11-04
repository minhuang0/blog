title: windows下的终端工具
date: 2016-08-15
tags: 
    - tools
categories: 编程

---



在windows下使用npm安装包和依赖，我觉得一个好的终端工具(命令行工具)是不可少的, windows下终端工具有不少:

- cmd
- Cmder
- git bash
- powershell（最近开源了）
- ConEmu
- Babun
- ...

cmd是windows系统自带的,个人觉得不好使用

git bash是安装windows git时安装上的命令行工具,能够输入一些linux命令如`ls -al`, 增加了主题

powershell封装了一些linux命令和一些windows命令

ConEmu包含了自己选择不同的shell,如 cmd, powershell, git bash,  bash。能够在一个窗口里面打开多个tabs(标签页),右键复制黏贴。

Babun是类似于一个虚拟机，打开后里面是虚拟的linux命令行环境,能够使用linux下的命令,能够配置zshell, 安装nvm, vim等等。大部分情况下是好用的，在调用一些windows下的工具是会有些path问题。

我通常是Babun ConEmu(powershell)混合着使用, 个人觉得前端涉及到node的时候还是换到mac或者linux下进行开发比较好。