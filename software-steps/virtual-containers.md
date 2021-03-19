---
title: 容器技术
description: Docker为主的容器技术
published: true
date: 2021-03-19T04:08:23.420Z
tags: docker, 容器, 系统运维, 软件使用
editor: markdown
dateCreated: 2021-02-03T12:22:34.981Z
---

# Docker容器技术
## Docker 安装

阿里云安装脚本。
```bash
curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun
```

## 配置镜像加速器
针对Docker客户端版本大于 1.10.0 的用户

您可以通过修改daemon配置文件/etc/docker/daemon.json来使用加速器
```bash
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://xxxxxx.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

## Docker常用命令

### 命令形式
- 镜像操作
```bash
//获取一个镜像
docker pull <image name>
//列出所有镜像
docker images
//删除一个镜像
docker rmi hello-world
```
- 容器操作
```bash
//列出所有容器
docker container list
//查看容器资料（包括容器所在的IP地址）
docker inspect <container-id>
//新建并启动容器 
docker run <>
//启动容器 
docker start <container-id>
//停止容器 
docker stop <container-id>
```
- 数据操作
```bash
//创建数据卷
 docker volume create my-vol
 //列出数据卷
 docker volume ls
//删除数据卷（不会物理删除）
docker volume rm my-vol
//清理数据卷
docker volume prune
```

- 从镜像中拷出拷入文件的操作
```bash
//镜像中往往没有编辑工具，因此需要对镜像中的文件进行拷入拷出操作
docker container ls //列出镜像，需要针对镜像ID拷入拷出，例如
docker cp 800aabc95413:/etc/mysql/mysql.cnf.d d:/Docker/dv/mysql.cnf.d
docker cp  D:\Docker\dv\mysql.conf.d\mysqld.cnf 800aabc95413:/etc/mysql/mysql.conf.d/mysqld.cnf
``
### 命令参数

参数名称|意义|示例|备注
---|---|---|---
run -i -t|i为交互式操作，t为终端|docker run -t -i ubuntu:14.04 /bin/bash|
-p |端口映射| -p 8000:80|前面一个为外部端口，后一个为容器内部端口
--name|容器命名|--name mynode|为容器命名
-v|挂载外部目录|-v my-vol:/usr/share/nginx/html|将my-vol挂载到容器中html目录

## Docker常见问题

### Docker如何连接宿主机中的数据库

在使用`bridge`桥接网络时，一般默认宿主机的ip地址为`172.17.0.1`，因此，在`Docker`中不能以`localhost`来连接宿主机中的数据库，而往往要把连接地址修改为上述地址。如果不确定宿主机在桥接网络中的地址，也可以通过在Docker终端中使用`ifconfig`或者`windows`系统下使用`ipconfig`查询。

## 使用Docker安装部分镜像的过程

说明，在windows的powershell和linux下续行符号是不一样的。以下\`符号，在linux下应该替换为\\。同样，如果在linux系统下，-v 后的卷标也要相应替换为linux目录。

### 1.安装运行mysql

```bash
docker run --name mysqltest `
-v F:\Databases\mysql\conf:/etc/mysql/conf.d `
-v F:\Databases\mysql\data:/var/lib/mysql `
-p 3306:3306 `
-e MYSQL_ROOT_PASSWORD=Taiyuan.666 mariadb
```

### 2.安装运行phpmyadmin

```bash
docker run --name myadmin `
--restart=always `
-d --link mysqltest:db `
-p 7080:80 phpmyadmin
```

### 3. 新建一个bridge网络
```bash
 docker network create -d bridge docker-net
```
 
### 4. 安装运行mongodb

```bash
docker run --name mongotest `
--restart always `
--network docker-net `
-v F:\Databases\mongo\data:/data/db `
-v F:\Databases\mongo\conf:/etc/mongo `
-p 7017:27017 `
-e MONGO_INITDB_ROOT_USERNAME=mongoadmin `
-e MONGO_INITDB_ROOT_PASSWORD=Taiyuan.666 `
-d mongo
```

### 5. 安装运行mongodb-express

```bash
docker run -it --rm `
    --network docker-net `
    --name mgexpress `
    -p 7081:8081 `
    -e ME_CONFIG_OPTIONS_EDITORTHEME="ambiance" `
    -e ME_CONFIG_MONGODB_SERVER="mongotest" `
    -e ME_CONFIG_MONGODB_ADMINUSERNAME="mongoadmin" `
    -e ME_CONFIG_MONGODB_ADMINPASSWORD="Taiyuan.666" `
    -e ME_CONFIG_BASICAUTH_USERNAME="user" `
    -e ME_CONFIG_BASICAUTH_PASSWORD="fairlypassword" `
    mongo-express
```
### 6. 安装运行mqtt(mosquitto)
```bash
docker run -it `
-p 1883:1883 -p 9001:9001 `
-v D:\docker\mqtt\conf:/mosquitto/config `
-v D:\docker\mqtt\data:/mosquitto/data `
-v D:\docker\mqtt\log:/mosquitto/log `
eclipse-mosquitto
```
