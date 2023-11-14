---
title: Docker安装
author: Xin Lu
date: '2023-11-13'
slug: []
categories: []
tags: []
---

excalidraw笔记绘板搭建

1，首先安装docker

2，安装docker-compose

```
yum -y install epel-release
yum install -y docker-compose
yum install python-pip
wget https://github.com/docker/compose/releases/download/1.14.0-rc2/docker-compose-Linux-x86_64
mv docker-compose-Linux-x86_64 /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
docker-compose -version


```



3，编写docker-compose.yaml文件

```
version: "3"
services:
  excalidrwa:
    image: excalidraw/excalidraw
    restart: unless-stopped
    ports:
      - 3000:80
```

4,启动excalidraw

```
docker-compose up -d
docker-compose ps    #查看端口
```



