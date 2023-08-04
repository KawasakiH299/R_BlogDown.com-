---
title: hadoop安装
author: Xin Lu
date: '2023-08-04'
slug: []
categories: []
tags: []
---

## hadoop安装

#### hadoop下载地址

Hadoop 下载地址：https://archive.apache.org/dist/hadoop/common/hadoop-3.1.3/ 



---

## 安装jdk

#### hadoop需要jdk环境

- 解压JDK 到/opt/module **目录下** 

```
[atguigu@hadoop102 software]$ tar -zxvf jdk-8u212-linux-x64.tar.gz -C /opt/module/ 
```

- 配置 **JDK** **环境变量** 
  - 新建/etc/profile.d/my_env.sh 文件 

```
[atguigu@hadoop102 ~]$ sudo vim /etc/profile.d/my_env.sh 

添加如下内容 

#JAVA_HOME 

export JAVA_HOME=/opt/module/jdk1.8.0_212 

export PATH=$PATH:$JAVA_HOME/bin 
```



- source 一下/etc/profile 文件，让新的环境变量 PATH 生效 

```
[atguigu@hadoop102 ~]$ source /etc/profile 
```





- 查看JDK **是否安装成功** 

```
[atguigu@hadoop102 ~]$ java -version 


如果能看到以下结果，则代表 Java 安装成功。 

java version "1.8.0_212"
```



---

## 安装hadoop

- 进入到 **Hadoop** **安装包路径下** 

```
[atguigu@hadoop102 ~]$ cd /opt/software/ 
```



- 解压安装文件到  /opt/module **下面** 

```
[atguigu@hadoop102 software]$ tar -zxvf hadoop-3.1.3.tar.gz -C  /opt/module/ 
```



- Hadoop **添加到环境变量** 
  - 获取 Hadoop 安装路径 

```
[atguigu@hadoop102 hadoop-3.1.3]$ pwd 

/opt/module/hadoop-3.1.3 
```



- 打开/etc/profile.d/my_env.sh 文件 

```
sudo vim /etc/profile.d/my_env.sh 


➢ 在 my_env.sh 文件末尾添加如下内容

#HADOOP_HOME 

export HADOOP_HOME=/opt/module/hadoop-3.1.3 

export PATH=$PATH:$HADOOP_HOME/bin 

export PATH=$PATH:$HADOOP_HOME/sbin 
```



- 让修改后的文件生效 

  ```
  [atguigu@hadoop102 hadoop-3.1.3]$ source /etc/profile 
  ```

  

 - 测试是否安装成功

```
[atguigu@hadoop102 hadoop-3.1.3]$ hadoop version 

Hadoop 3.1.3

```

- 重启（如果Hadoop命令不能用再重启虚拟机）

  [atguigu@hadoop102 hadoop-3.1.3]$ sudo reboot 