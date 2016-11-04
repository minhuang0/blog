title: npm如何改变源地址
date: 2016-08-25
tags: 
    - tools
    - npm
categories: 编程

---

由于墙的关系,默认的npmjs.com的源则会严重拖慢安装包的速度,也会产生由文件没下载完整后一些安装不上的error,可以通过替换源的方式来解决这个问题

下面是3种替换源的方式:

- npm config命令

```
 $npm config set registry https://registry.npm.taobao.org 
```

- 每次安装的时候加上地址参数: `--registry 源地址`

```
$ npm --registry https://registry.npm.taobao.org install -g cnpm
```

- 添加 ~/.npmrc 配置文件并在里面加上如下内容(linux、Mac下有效)

```
registry = https://registry.npm.taobao.org  
```

如果不想替换源的方式可以使用 `[cnpm](https://npm.taobao.org/)`安装,

```
$npm install -g cnpm --registry=https://registry.npm.taobao.org
```

安装完成后使用cnpm代替npm安装

```
$ cnpm install
```