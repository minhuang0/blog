title: 在window下面搭建一个hexo的blog
date: 2016-08-18
tags: 
    - hexo
categories: 编程

---

我们需要准备的:

- Windows
- [Git](https://git-scm.com/downloads)
- [ConEmu](https://conemu.github.io/)
- [NodeJs](https://nodejs.org/zh-cn/)
- [GitHub](http://github.com/)

<!--more-->  

### 安装Hexo:

- 安装ConEmu终端工具,比cmd好用点。（如果习惯了cmd也可以忽略这一步）

- 安装Git Windows版本(安装完成后能够运行git命令，在cmd或ConEmu下都行)
安装git完成后首先需要初始化自己全局的用户名和邮箱setting [email](https://help.github.com/articles/setting-your-email-in-git/) and [username](https://help.github.com/articles/setting-your-username-in-git/) in Git
```
$git config --global user.name "your_user_name"
$git config --global user.email "your_email@example.com"
```

- 安装NodeJs Windows版本(这里就直接安装node了，不装nvm管理node版本了)

在命令行中输入
```
$node -v

```
此时能够正确返回版本号则说明安装成功

- Node安装后安装[hexo](https://hexo.io/zh-cn/)

在终端工具(ConEmu,cmd Or 其他)中运行命令(此时的$代表终端命令，不需要实际输入)
```
$npm install hexo-cli -g
$hexo init blog
$cd blog
$npm install
$hexo server
```
此时并可以启动一个本地的服务

### 创建GitHub repository

仓库名字为:
```
你的GitHub账号名.github.io
```
如我的是
```
minhuang0.github.io
```

创建完成后我们会得到一个远程地址(点击SSH时页面会改为ssh地址):
```
https://github.com/minhuang0/minhuang0.github.io // or git@github.com:minhuang0/minhuang0.github.io.git
```

此时仓库创建完成，我们需要将代码部署到github上面去

手动方式是到刚才`/blog/public`目录下面将代码`push`到远程地址
自动方式往下看。

### 部署代码

幸运的是hexo已经为我们准备好了[多种部署方案](https://hexo.io/zh-cn/docs/deployment.html)。

- 安装部署pluging

```
 $npm install hexo-deployer-git --save

```


- 我们需要在`/blog/_config.yml`下面配置deploy参数

例如我的配置是以git方式部署到`https://github.com/minhuang0/minhuang0.github.io`地址的主分支上面。

```
deploy:
  type: git
  repository: https://github.com/minhuang0/minhuang0.github.io
  branch: master

```

- 将markdown文件编译

```
$hexo g
```

- 将public目录下面的文件推送到你的git repository
```
$hexo deploy
```

- 在浏览器中输入: `你的GitHub账号名.github.io` 则会出现刚才你部署的内容