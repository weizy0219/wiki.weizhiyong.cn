---
title: 数据库
description: 数据库相关软件操作使用步骤
published: true
date: 2021-02-26T00:45:14.675Z
tags: 操作步骤, 数据库, 编程技巧, 软件使用
editor: markdown
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

# MongoDB 数据库

## 连接数据库

在`mongoDB`的连接字符串中，如果包含了特殊字符，需要通过[百分比编码](/fav-lists/percent-encoding)来对特殊字符进行转义。

- 标准URI连接方案具有以下形式：
```bash
mongodb://[username:password@]host1[:port1][,...hostN[:portN]]][/[database][?options]]
```
- 对于独立MongoDB:
```bash
mongodb://mongodb0.example.com:27017/admin
```
- 如果开启了访问控制(此处的`%40`为百分比编码)：
```bash
mongodb://myDBReader:D1fficultP%40ssw0rd@mongodb0.example.com:27017/admin
```
如果用户名或密码包含at符号@，冒号：，斜杠/或百分号％字符，请使用百分比编码方式消除歧义
- 对于副本集群:
```bash
mongodb://mongodb0.example.com:27017,mongodb1.example.com:27017,mongodb2.example.com:27017/admin?replicaSet=myRepl
```
- 如果开启了访问控制，请包括用户凭据：
```bash
mongodb://myDBReader:D1fficultP%40ssw0rd@mongodb0.example.com:27017,mongodb1.example.com:27017,mongodb2.example.com:27017/admin?replicaSet=myRepl
```
