title: 使用nginx来配置我的blog
date: 2015-03-16
tags: 
    - rails
    - nginx
categories: 编程

---

这里仅作笔记，不做教程，[nginx wiki](http://wiki.ubuntu.org.cn/Nginx)的更加详细噢.
<!--more-->  

以huangmin.me的rails blog部署在ubuntu系统下为例子：

- 首先是需要安装nginx了 。

```
sudo apt-get install nginx
```

- 需要在 /etc/nginx/nginx.conf(当然不一定是这个路径,有的可以配置在/etc/nginx/sites-available/目录下新建自己的一个配置可以)中添加如下代码:

```
server {
  listen       80;  //监听的端口
  server_name www.huangmin.me huangmin.me; //解析的域名
  charset utf-8;
  location / { 
    proxy_pass          http://huangmin_servers;
    proxy_redirect      default;
    proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header    X-Real-IP $remote_addr;
    proxy_set_header    Host $http_host;
    proxy_next_upstream http_502 http_504 error timeout invalid_header;
  }
}

upstream huangmin_servers{
    server localhost:2333; //转发的端口，这里跑在localhost:2333上面，所以只需指向本地即可。如果是在路由器的环境下面，可以指向一个内网的ip地址，并指向端口。
    server localhost:2334;
}
```

- 平缓重启Nginx

```
$cd /etc/nginx/
//平缓重启
$nginx -s reload
//停止
$nginx -s stop 
//启动
$nginx
$nginx start
//测试 
$nginx -t 
```

- 在自己购买的域名服务商处更改自己的域名解析IP地址,指向项目服务器的公网地址。
