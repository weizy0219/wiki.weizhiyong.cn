---
title: Linux
description: Linux系统相关操作与命令
published: true
date: 2021-02-05T13:27:26.267Z
tags: linux, shell, 系统运维, 软件使用
editor: markdown
dateCreated: 2021-02-04T04:16:07.771Z
---

# 命令行
## 用户管理

- 添加用户`username`
```bash
sudo useradd -g vsftpd -d /share/vsftpd -m username
```
参数名称|含义
---|---
-g|添加到用户组(`vsftpd`)
-d|设置用户根目录
-m|不建立默认根目录

- 修改用户`username`的密码
```sudo
sudo passwd username
```


## `tar`压缩和解压

### 解压缩和压缩
```bash
//解压缩
tar -zxvf abc.tar
//压缩
//压缩 a.c文件为test.tar.gz
tar -zcvf test.tar.gz a.c   
```

### 常用参数
参数名称|含义
---|---
z | 是否同时具有 gzip 的属性
j | 是否同时具有 bzip2 的属性
x | 解压缩
c | 压缩（z和x区分压缩和解压）
v | 压缩的过程中显示文件
f | 使用档名,f之后要直接接文档名

## `SSH`加密通道通讯(Secure Shell)

### 生成`SSH`密钥

以指定邮箱生成密钥对。
```bash
ssh-keygen -t rsa -C "your_email@example.com"

//默认的公钥和密钥存储在以下目录
~/.ssh/id_rsa.pub
~/.ssh/id_rsa.
```
### 复制密钥到远程主机

```bash
ssh-copy-id -p 1234 user@<host>
```
-p 1234 为通过1234连接。也可以通过 -i 指定密钥文件。
复制密钥（公钥）到远程主机之后就可以免密登录

### 通过SSH连接主机
```bash
ssh -p 2222 user@<host>
```
-p 2222 为通过2222端口连接

### 重启ssh服务

```bash
// ubuntu系统
service ssh restart

// debian系统
/etc/init.d/ssh restart
 ```
 
 ### 配置`SSH`服务
 通过`~/.ssh/config`文件配置SSH服务。格式如下：
 ```bash
Host wifi
Hostname 192.168.1.111
User root
Port 22
IdentityFile ~/.ssh/keys/dsl.key
 ```
