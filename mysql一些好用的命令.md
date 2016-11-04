title: mysql一些好用的命令
date: 2015-03-16
tags: 
    - mysql

categories: 编程

---

- 数据库导出

```
mysqldump -u root happystock > happstock_2014_10_10.sql 
```
<!-- more -->
- 数据库导入

```
mysql -u root happystock_2014_10_10.sql < happystock;
```
- 删除表数据

```
TRUIVCATE TABLE '表名'
```
- 删除数据库

```
DROP DATABASE IF EXISTS happystock_test;
```