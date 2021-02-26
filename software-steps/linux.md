---
title: Linux
description: Linux系统相关操作与命令
published: true
date: 2021-02-26T13:20:07.391Z
tags: linux, shell, 系统运维, 软件使用
editor: markdown
dateCreated: 2021-02-04T04:16:07.771Z
---

# linux常用操作（以Ubuntu为主）
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

- 删除用户
```bash
sudo userdel vsftpd
```

- 修改用户`username`的密码
```bash
sudo passwd username
```
- 查看用户id
```bash
id username
```
- 修改用户主目录
需要注意，下面的`uid`是前一步用`id`命令获取的用户uid
```bash
usermod -d /usr/newfolder -u uid username
```
## `ufw`防火墙

```bash
# 允许端口或端口范围
sudo ufw allow 20:21/tcp
sudo ufw allow 30000:31000/tcp
# 允许服务
sudo ufw allow OpenSSH
#通过禁用和重新启用UFW重新加载UFW规则：
sudo ufw disable
sudo ufw enable
```
要验证更改，请运行：
```bash
sudo ufw status
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

## `SCP`跨主机复制文件

从SRC_HOST复制文件或目录到DEST_HOST
```bash
scp [OPTION] [user@]SRC_HOST:]file1 [user@]DEST_HOST:]file2
```
【OPTIONS】参数名称|含义
---|---
-P|指定远程主机ssh端口（ssh命令是小写p，这里是大写）
-p|保留文件修改和访问时间。
-q|如果要禁止显示进度表和非错误消息，请使用此选项。
-C|此选项将强制scp在将数据发送到目标计算机时对其进行压缩。
-r|此选项将告诉scp递归复制目录。

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

## 通过`vsftp`架设`ftp`服务器

### 安装与删除`vsftp`
```bash
//安装
sudo apt update 
sudo apt install vsftpd
//删除
sudo apt-get remove --purge vsftpd
sudo userdel vsftpd //同时删除为ftp新建的用户
```
### `vsftp`进程管理

可以通过以下三种方式查看或管理`vsftp`进程
```bash
service vsftpd start|stop|restart|status
systemctl start|stop|restart|status vsftpd
/etc/init.d/vsftpd start|stop|restart|status|reload
```

### 配置文件及修改

默认的配置文件目录`/etc/vsftpd.conf`。**修改该文件并重启服务以生效配置**
默认的ftp目录 `srv/ftp`。

- 常用配置项
```bash
#允许匿名用户登录，建议为NO
anonymous_enable=NO
#允许本机现有用户登录，可以配置为YES，并新增用户
local_enable=YES
#允许上传文件，应该为YES
write_enable=YES
#以下两个配置组合来确定是否允许本地用户切换到主目录之外
#如下配置是禁止所有用户切换到主目录之外
chroot_local_user=YES
chroot_list_enable=NO
#如果上一个选项为YES，则需要新建以下文件并在其中列出例外的用户名
chroot_list_file=/etc/vsftpd.chroot_list
#欢迎信息
ftpd_banner=Welcome, Visit www.weizhiyong.com for more info.
```

- 自定义配置项
以下配置项在配置文件中没有，可以根据需要增加
```bash
listen_port=6666   #修改ftp端口为6666
local_root=/ftp    #配置本地用户主ftp目录
allow_writeable_chroot=YES #如果root目录为可写，需要配置此项，否则会出现500/501错误
utf8_filesystem=YES #设置utf8编码

#使能被动模式并指定被动模式端口
pasv_enable=YES
pasv_max_port=21020
pasv_min_port=21001
```

## SCP远程复制文件
语法
```bash
scp [-1246BCpqrv] [-c cipher] [-F ssh_config] [-i identity_file]
[-l limit] [-o ssh_option] [-P port] [-S program]
[[user@]host1:]file1 [...] [[user@]host2:]file2
```
简易写法:
```bash
scp [可选参数] file_source file_target 
```
