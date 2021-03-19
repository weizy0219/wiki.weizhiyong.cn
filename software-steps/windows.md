---
title: windows
description: windows 操作系统相关用法
published: true
date: 2021-03-19T05:55:38.831Z
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

## WSL linux子系统

操作教程：[Windows10安装与配置WSL2及Docker](https://www.weizhiyong.com/archives/4354)

### 安装与配置

```bash
//启用“适用于 Linux 的 Windows 子系统”可选功能
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

//启用虚拟机平台可选功能
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart

//设置WSL2为默认版本
wsl --set-default-version 2

//配置某个版本的Linux为WSL 2 (例如Ubuntu-18。04)
wsl --set--version <Ubuntu-18.04> 2

//设置默认的WSL系统Linux版本
wsl -s <DistributionName>
在Windows商店中搜索Linux（或Ubuntu）并进行安装，一般来说建议默认安装Ubuntu。
```

### 常用WSL管理行命令
```bash
//查看安装的wsl版本列表
wsl -l -v
//配置某个linux发行版为版本2
wsl --set-version (distro name) 2
//配置wsl默认版本为版本2
wsl --set-default-version 2
//以某个特定用户运行某一个发行版
wsl -u <Username>
//注销（卸载）某个发行版以重新安装
wsl --unregister <DistributionName>
//为某个发行版配置默认用户
<DistributionName> config --default-user <Username>
//停止所有正在运行的WSL子系统
wsl --shutdown 
```

### 解决WSL2中Vmmem内存占用过大问题
新建wsl配置文件 `%UserProfile%\.wslconfig` (可以cd到%UserProfile%\也就是用户主目录下新建该文件)。
通过修改memory文件和swap值，修改存储限制。
```bash
[wsl2]
memory=4GB
swap=8GB
localhostForwarding=true
```