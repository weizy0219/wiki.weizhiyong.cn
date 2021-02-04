---
title: Linux
description: Linux系统相关操作与命令
published: true
date: 2021-02-04T07:15:37.499Z
tags: 
editor: undefined
dateCreated: 2021-02-04T04:16:07.771Z
---

# 命令行

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
