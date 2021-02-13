---
title: 2.计算机使用技巧
description: 
published: true
date: 2021-02-13T15:31:35.360Z
tags: windows, 微软, 软件使用
editor: markdown
dateCreated: 2021-02-03T03:36:17.562Z
---

# 计算机使用技巧

## [C盘容量不够的解决办法](/software-howtos/windows-c-disk)
## 笔记本方向键怎么使用才能当HOME、END

Home：fn + ←

End：fn + →

PgUp：fn + ↑

PgDn：fn + ↓

## MicroSoft Project

### MicroSoft Project修改工作日和非工作日的方法

在“项目”->“属性”->“更改工作时间”选项下。可以修改某一天为工作日或者非工作日。

![projectsetworkingdate.png](/projectsetworkingdate.png){.align-center}

### MicroSoft Project设置工作周期为自然日或工作日

- 在Project中，“天”和“工作日”分别对应自然日和工作日。
- 双击任务名称，在“工期”栏里面输入“60 天“即为自然日，输入“60 工作日”即自动调整为工作日。
- 如果日期为估算，可以选中后方的估算框，日期栏中会出现问号标志。
- 双击“自动计划”可以自动调节日期，在“前置任务”中输入前置任务标号，可以设置任务先后顺序和关系。

## 将VScode添加至右键菜单
如果在安装时没有选择将VSCode添加到右键菜单，也可以通过以下命令进行。
- 1. 右击VScode快捷方式查看属性，找到快捷方式对应的目标路径

![](https://img-blog.csdnimg.cn/20200101140653735.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2thbmd5dXBs,size_16,color_FFFFFF,t_70)

- 2. 随便找个地方新建个XXX.reg的注册表脚本文件，文件名叫啥都可以，但后缀名必须为.reg，然后在里面粘贴上下面的代码.
**路径需要替换为你的Code的安装路径**.

```reg
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\*\shell\VSCode] ;右击文件时弹出的菜单
@="Edit with Visual Studio Code" ;显示的文字
"Icon"="D:\\Microsoft VS Code\\Code.exe" ;显示的图标

[HKEY_CLASSES_ROOT\*\shell\VSCode\command] ;要执行的命令
@="\"D:\\Microsoft VS Code\\Code.exe\" \"%1\"" ;具体的命令代码，%1代表第一个参数，即右击选中的那个文件的路径

Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\Directory\shell\VSCode] ;右击文件夹时弹出的菜单
@="Open with Visual Studio Code"
"Icon"="D:\\Microsoft VS Code\\Code.exe"

[HKEY_CLASSES_ROOT\Directory\shell\VSCode\command]
@="\"D:\\Microsoft VS Code\\Code.exe\" \"%V\"" ;%V意思同%1，只不过在路径为空时替换为当前工作路径
```
粘贴完成后再将代码里的Code.exe路径替换为前面我们在属性里看的那个Code.exe路径，注意" \ “要转换为” \\ "
- 3.保存文件，双击执行，一路选是，完成.

## HTML

### 怎样在页面中添加网站标题前的logo
1. 准备一张图片并且通过在线转换网站转换为ico文件
	- [faviconico](http://www.faviconico.org/favicon)

2. 在<head></head>标签中添加如下代码：
```html
<link rel="icon" type="image/x-ico" href="./static/image/cc.ico" />
```
