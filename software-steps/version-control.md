---
title: 版本管理
description: 版本管理git软件常用操作步骤
published: true
date: 2021-02-03T12:05:57.953Z
tags: 
editor: undefined
dateCreated: 2021-02-03T12:05:52.493Z
---

# Git版本管理

## git 常用操作

### 配置全局参数

```bash
git config --global user.name "weizy@126.com"
git config --global user.email ""
```

### 初始化项目

```bash
git init
```


## 如何将本地项目推送到远程新建的空项目仓库中

### 方式一：克隆仓库
```bash
git clone 
https://codeup.aliyun.com/5f608530df9df74e36b017d4/opencv_3rdparty.git
cd opencv_3rdparty
touch README.md
git add README.md
git commit -m "add README"
git push -u origin master
```

### 方式二：已有文件夹或仓库
```bash
cd existing_folder
git init
git remote add origin https://codeup.aliyun.com/5f608530df9df74e36b017d4/opencv_3rdparty.git
git add .
git commit
git push -u origin master
```

### 方式三：导入代码库
```bash
git clone --bare https://git.example.com/your/project.git your_path
cd your_path
git remote set-url origin https://codeup.aliyun.com/5f608530df9df74e36b017d4/opencv_3rdparty.git
git push --mirror
```
## git 技巧
### 如何恢复`git stash`命令
如果不小心使用了`git stash`命令而大部分工作都没有保存，可以使用以下pop来恢复
```bash
git stash pop
```

### git如何保持fork后的项目和源项目同步更新

1. 查看远程状态

```
git remote -v
```

2. 添加远程的上游仓库 

```
git remote add upstream https://github.com/XXX/XXX.git
```

3. 再次查看状态确认是否配置成功

```
git remote -v
```

4. 同步fork

从上游仓库 fetch 分支和提交点，提交给本地 master，并会被存储在一个本地分支 upstream/master 

```
git fetch upstream
```

5. 切换到本地主分支(如果不在的话) 

```
git checkout master
```

6. 把 upstream/master 分支合并到本地 master 上，这样就完成了同步，并且不会丢掉本地修改的内容。

```
git merge upstream/master
```

7. 更新到 GitHub或其他远程git仓库上

```
git push origin master
```