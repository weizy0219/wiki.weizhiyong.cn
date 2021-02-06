---
title: windows
description: windows 操作系统相关用法
published: true
date: 2021-02-06T07:52:24.306Z
tags: windows, 操作系统, 软件使用
editor: markdown
dateCreated: 2021-02-03T10:10:13.010Z
---

# Windows操作系统问题
## 命令行常用操作

`Win+R`快捷键打开命令窗口。

### 查看内存

```cmd
wmic memorychip
```

### 开启`OpenSSH`服务

- 在“设置”-->“应用”-->“应用和功能”-->“管理可选功能”-->"添加可选功能“中找到OpenSSH并安装。
![openssh.png](/images/2021/openssh.png)

- 搜索“服务”，在服务中将以下两项设为自动启动。
```bash
 OpenSSH Authentication Agent
 OpenSSH SSH Server 
 ```
- 通过以下命令可以管理ssh服务器启停
```bash
net start sshd
net stop sshd
```

之后就可以通过ssh客户端以常规方式访问了。注意，如果你的windows用户名是微软账户（邮箱的话）需要输入完整地址，如下示意，但在你登录之后，邮箱后面的部分是不显示的。这是和原生的linux下的openssh区别的地方。
```bash
ssh weixx@outlook.com@192.168.1.8
```