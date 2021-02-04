---
title: 数据库
description: 数据库相关软件操作使用步骤
published: true
date: 2021-02-03T09:14:52.250Z
tags: 
editor: undefined
dateCreated: 2021-02-03T09:14:46.770Z
---

# MySQL数据库

MySQL数据库操作完成后记得使用`flush privileges`刷新权限。

### 以管理员身份登录数据库

```bash
mysql -u root -p
```

### MySql修改用户主机从%到localhost

```bash
UPDATE mysql.user SET Host='%' WHERE Host='localhost' AND User='username';
FLUSH PRIVILEGES;
```
### 授予用户root远程访问数据库的权限

```bash
//设置用户root，可以在远程访问mysql
grant all privileges on *.* to root@”%” identified by “123456” ;　　　
```
### 查询mysql中所有用户权限
```bash
use mysql;
select host,user from user;
```

### 修改指定用户密码
```bash
update mysql.user set password=password('新密码') where User="zs" and Host="localhost";
flush privileges;
```
