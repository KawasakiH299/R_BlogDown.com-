---
title: Docker安装
author: Xin Lu
date: '2023-07-21'
slug: []
categories: []
tags: []
---

### 安装docker

#### 安装docker依赖环境：

```
yum install -y yum-utils device-mapper-persistent-data lvm2
```

#### 配置国内docker-ce的yum源（这里采用的是阿里云）

```
yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

- [yum-config-manager命令作用是添加yum源。
  敲完命令之后执行以下命令去看一下有没有配置成功。
  cd /etc/yum.repos.d
  ls]()



#### 安装docker。

```
yum -y install docker-ce doker-ce-cli containerd.io
```



---

### 使用docker

#### 启动服务。

```
systemctl start docker 
```

#### docker状态

```
systemctl status docker
```

#### 停止服务

```
systemctl stop docker
```





#### 镜像

```
docker pull centos


[下载最新的CentOS镜像]
```



#### 查看镜像

```
docker images
```



#### 创建并启动容器

```
docker run -dit --name server1(别名) 镜像名称
```

#### 删除镜像

```
docker rmi 镜像id
```





#### 停止docker

```
systemctl stop docker 
```



#### 查看容器列表

```
docker ps -a
```



#### 启动容器

```
sudo docker start 容器id
docker start ubuntu01 #通过名称启动容器
```

#### 退出容器

```
exit

docker stop 容器id

ctrl + D
```

#### 删除容器

``



#### 进入启动的容器

```
docker exec -it 容器id  /bin/bash
docker attach ubuntu01 #进入容器   -i:交互式
```



#### 停止容器

```
systemctl  stop  docker 
```

### 容器导出

- 将ubuntu 的容器导出到文件ubuntu_run.tar中：

```
docker export -o testroqi.tar ubuntu-01
```



- 可以使用scp 指令将文件进行传送：`scp ubuntu_run.tar root@124.207.96.94:/root/`



---

### 容器导入

另外 docker load 命令也可以导入一个镜像存储文件，但是跟docker import 命令是有区别的：

- docker import：丢弃了所有的历史记录和元数据信息，仅保存容器当时的快照状态。在导入的时候可以重新制定标签等元数据信息。

- docker load：将保存完整记录，体积较大。

  ```
  docker import testroqi.tar test（镜像名）
  ```

  #### docker 推到私有仓库

  #### docker -commit



#### docker 日志

```
docker logs 容器名
```



#### docker数据卷绑定

```
将linux文件自同步到容器中的目录
```

```
docker run -itd --name 容器别名 -v /var/scrapy_text:/usr/src
docker -v linux宿主机路径：容器文件夹路径



你提供的Docker命令是一个用于运行容器的示例。下面是对该命令的解释：

```
docker run -itd --name <容器别名> -v /var/scrapy_text:/usr/src <镜像名称>
```

- `docker run` 是运行容器的命令。
- `-itd` 参数用于创建一个交互式的终端并在后台运行容器。
- `--name <容器别名>` 参数用于指定容器的别名或名称。
- `-v /var/scrapy_text:/usr/src` 参数用于将主机的`/var/scrapy_text`目录挂载到容器内的`/usr/src`目录，实现主机和容器之间的文件共享。
- `<镜像名称>` 是你要运行的容器所基于的镜像名称。

```



#### docker根据Dockerfile新建容器并配置项目环境

```
docker build .(当前路径) -t 容器别名 -f Dockerfile 容器镜像
```