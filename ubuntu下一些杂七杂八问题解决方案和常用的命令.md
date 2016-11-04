title: ubuntu下重启sougou、Android手机无权限等问题解决方案
date: 2015-03-16
tags: 
    - ubuntu

categories: 编程

---

### ubuntu下无痛重启搜狗输入法,用过的人都说好:
<!-- more -->
```
$pidof fcitx
$fcitx &
$sogou-qimpanel &
```
其他,下面是一些Ubuntu下面问题的解决方案

### 修改文件权限
```
chmod -R 755 fileName
```

### android手机无权限问题

```
adb deviceslsusb  
//记住ID后面到两个四位 16进制数
sudo vim /etc/udev/rules.d/
//增加一个
usb:SUBSYSTEM='user',ATTRS{idVendor}=="18d1",ATTRS{id Product} == "9025",MODE='0666'
//给权限：
sudo chmod a+rx /ect/udev/rules.d/70-android.rules
//重启udev:
sudo service udev restart
//重启
adb server:kill  
//启动：
adb server
```

### 清理理缓存

```
$sync

$echo 3 > /proc/sys/vm/drop_cache
```

### 软链接

ln -s 源地址 目的地

这个命令经常用的到，老是会搞反目标地址和当前地址,记录一下.



### SCP上传文件到服务器

scp -r -p 当前目录 目标地址

scp -P 1080 -r files root@106.xx.x.x:/opt/app/huangmin 

以root账户登录106.xx.x.x服务器，并放到/opt/app/huangmin 目录下面

-r指files的全部内容

-P 指的端口1080


### UTF-8等编码错误


在 `~/.bashrc`(如果是zsh,为~/.zshrc)中添加

```
export LANG = en_US.UTF-8

export LC_ALL = en_US.UTF-8

export LANGUAGE = en_US.UTF-8
```

再次刷新 
```
$source ~/.bashrc
```

Liunx自动执行工具

```
nohub ruby scheduler.rb &

tail nohup.log
```

### 查看服务器挂载：

```
df -kh
```

### 定时执行：crontab -e

例：每分钟备份文件：

```
* * * * * rsync -arv /files/ ubuntu@192.168.88.1xx:/files/
```
### grep查询

```
grep -r 'set_devies_adaptation' . 
```
//查询某个文件夹下所有文件中含有set_devies_adaptation的文件