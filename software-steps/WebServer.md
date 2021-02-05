---
title: 网络服务
description: nginx,apache等技术
published: true
date: 2021-02-05T17:06:23.982Z
tags: 网络, 服务器, http, nginx, apache
editor: markdown
dateCreated: 2021-02-05T17:06:23.982Z
---

# Nginx 安装及配置

```bash
sudo apt-get install nginx
```
配置文件位于`/etc/nginx`,在`sites-enabled`目录下有默认配置。

## 使用`Let’s Encrypt`的`certbot`工具启用网站https

首先需要将域名解析到服务器、

- 安装`snapd`并通过`snapd`安装certbot
```
#如果系统没有安装
sudo apt-get install snapd
#更新snapd
sudo snap install core; sudo snap refresh core
#移除已经安装的certbot
sudo apt-get remove certbot
#通过snap安装certbot
sudo snap install --classic certbot
#配置certbot软连接
sudo ln -s /snap/bin/certbot /usr/bin/certbot
```
- 修改`nginx`域名并通过`certbot`自动配置https
如果域名配置在`default`文件中，则需要对配置文件做如下修改。解析在同一位置的不同域名通过空格隔开。这样`certbot`可以识别不同的域名。如果域名配置在不同文件中，则certbot可以分别自动识别各个域名。
```bash
server {
	server_name irisap.com www.irisap.com;
  ... ...
```
通过certbot自动配置nginx,以下命令可以自动配置nginx域名，根据命令行提示输入邮箱地址，以确定更新域名证书时的邮箱，可以配置邮箱是否公开，可以在certbot列出的域名中选择要配置哪几个域名（通过空格或者逗号隔开选择），`certbot`会自动配置域名并配置自动更新,该命令执行后,http请求会自动转向https。
```bash
sudo certbot --nginx
```
如果仅仅要`certbot`生成证书，手动配置其他内容（不推荐），使用如下命令：
```bash
sudo certbot certonly --nginx
```
通过以下命令验证certbot是否可以正常定期更新证书。
```bash
sudo certbot renew --dry-run
```