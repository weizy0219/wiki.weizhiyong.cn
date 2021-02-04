---
title: 2.计算机使用技巧
description: 
published: true
date: 2021-02-04T12:09:51.604Z
tags: 
editor: undefined
dateCreated: 2021-02-03T03:36:17.562Z
---

# 计算机使用技巧

## MicroSoft Project

### MicroSoft Project修改工作日和非工作日的方法

在“项目”->“属性”->“更改工作时间”选项下。可以修改某一天为工作日或者非工作日。

![projectsetworkingdate.png](/projectsetworkingdate.png){.align-center}

### MicroSoft Project设置工作周期为自然日或工作日

- 在Project中，“天”和“工作日”分别对应自然日和工作日。
- 双击任务名称，在“工期”栏里面输入“60 天“即为自然日，输入“60 工作日”即自动调整为工作日。
- 如果日期为估算，可以选中后方的估算框，日期栏中会出现问号标志。
- 双击“自动计划”可以自动调节日期，在“前置任务”中输入前置任务标号，可以设置任务先后顺序和关系。


## HTML

### 怎样在页面中添加网站标题前的logo
1. 准备一张图片并且通过在线转换网站转换为ico文件
	- [faviconico](http://www.faviconico.org/favicon)

2. 在<head></head>标签中添加如下代码：
```html
<link rel="icon" type="image/x-ico" href="./static/image/cc.ico" />
```
