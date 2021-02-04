---
title: JavaScript
description: JavaScript,nodejs相关库与软件操作步骤
published: true
date: 2021-02-03T14:17:26.512Z
tags: 
editor: undefined
dateCreated: 2021-02-03T09:30:06.897Z
---

# Nodejs

## [PM2](https://www.npmjs.com/package/pm2) 常用命令

### PM2安装

- 通过npm安装
```bash
npm install pm2 -g
```
- 通过linux命令行安装

```bash
wget -qO- https://getpm2.com/install.sh | bash
```

### 进程管理
- 启动进程，被启动的程序在中断后会自动恢复运行
```bash
pm2 start app.js
```
- 进程管理
```bash
//列出所有管理的进程
pm2 list
//停止指定进程
pm2 stop     <app_name|namespace|id|'all'|json_conf>
//重启指定进程
pm2 restart  <app_name|namespace|id|'all'|json_conf>
//删除指定进程
pm2 delete   <app_name|namespace|id|'all'|json_conf>
//查看进程详情
pm2 describe <id|app_name>
//重启所有进程
pm2 reload all
//指定进程数
$ pm2 start api.js -i <processes>
```
### 进程记录
```bash

pm2 logs APP-NAME       # 显示APP-NAME的记录
pm2 logs --json         # 以JSON输出记录
pm2 logs --format       # 格式化输出记录

pm2 flush               # 刷新所有记录
pm2 reloadLogs          # 重启所有记录
```

### 生成开机自启动文件

```bash
# 生成启动脚本，可能要按照命令行提示进行后续步骤操作
$ pm2 startup

# 将当前监控的进程列表保存到开机启动列表中
$ pm2 save

# 解除（删除）自动启动脚本
$ pm2 unstartup
```





