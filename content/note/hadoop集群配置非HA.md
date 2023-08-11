---
title: hadoop集群配置非HA
author: Xin Lu
date: '2023-08-09'
slug: []
categories: []
tags: []
---



### Haddop配置文件分为两类：

- 默认配置文件

| 默认文件  | 文件存放在hadoop的jar包中的位置 |
| -------- | ------------------------------- |
| core-default.xml | hadoop-common-3.1.3.jar/core-default.xml |
| hdfs-default.xm | hadoop-hdfs-3.1.3.jar/hdfs-default.xml |
| yarn-default.xml | hadoop-yarn-common-3.1.3.jar/yarn-default.xml |
| mapred-default.xm | hadoop-mapreduce-client-core-3.1.3.jar/mapred-default.xml |
| | |

- 自定义配置文件
  - core-site.xml
  - hdfs-site.xml
  - yarn-site.xml
  - mapred-site.xml



---

### ssh免密登录：

```
（2）生成公钥和私钥
[atguigu@hadoop102 .ssh]$ pwd
/home/atguigu/.ssh
[atguigu@hadoop102 .ssh]$ ssh-keygen -t rsa
然后敲（三个回车），就会生成两个文件 id_rsa（私钥）、id_rsa.pub（公钥）
（3）将公钥拷贝到要免密登录的目标机器上
[atguigu@hadoop102 .ssh]$ ssh-copy-id hadoop102
[atguigu@hadoop102 .ssh]$ ssh-copy-id hadoop103
[atguigu@hadoop102 .ssh]$ ssh-copy-id hadoop104
```

---

### 核心配置文件

#### 核心配置文件

##### core-site.xml

```
<?xml version="1.0" encoding="UTF-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<configuration>
 <!-- 指定 NameNode 的地址 -->
 <property>
 <name>fs.defaultFS</name>
 <value>hdfs://hadoop102:8020</value>
 </property>
 <!-- 指定 hadoop 数据的存储目录 -->
 <property>
 <name>hadoop.tmp.dir</name>
 <value>/opt/module/hadoop-3.1.3/data</value>
 </property>
 <!-- 配置 HDFS 网页登录使用的静态用户为 atguigu -->
 <property>
 <name>hadoop.http.staticuser.user</name>
 <value>atguigu</value>
 </property>
</configuration>
```



#### HDFS配置文件

##### hdfs-site.xml

```
<?xml version="1.0" encoding="UTF-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<configuration>
<!-- nn web 端访问地址-->
<property>
 <name>dfs.namenode.http-address</name>
 <value>hadoop102:9870</value>
 </property>
<!-- 2nn web 端访问地址-->
 <property>
 <name>dfs.namenode.secondary.http-address</name>
 <value>hadoop104:9868</value>
 </property>
</configuration>
```



#### YARN配置文件

##### yarn-site.xml

```
<configuration>
 <!-- 指定 MR 走 shuffle -->
 <property>
 <name>yarn.nodemanager.aux-services</name>
 <value>mapreduce_shuffle</value>
 </property>
 <!-- 指定 ResourceManager 的地址-->
 <property>
 <name>yarn.resourcemanager.hostname</name>
 <value>hadoop103</value>
 </property>
 <!-- 环境变量的继承 -->
 <property>
 <name>yarn.nodemanager.env-whitelist</name>
 
<value>JAVA_HOME,HADOOP_COMMON_HOME,HADOOP_HDFS_HOME,HADOOP_CO
NF_DIR,CLASSPATH_PREPEND_DISTCACHE,HADOOP_YARN_HOME,HADOOP_MAP
RED_HOME</value>
 </property>
</configuration>
```

#### MapReduce配置文件

####   mapred-site.xml

```
<configuration>
<!-- 指定 MapReduce 程序运行在 Yarn 上 -->
 <property>
 <name>mapreduce.framework.name</name>
 <value>yarn</value>
 </property>
</configuration>
```

---

### **群起集群** 

#### 配置hadoop/etc/hadoop/workers文件

vim  /opt/module/hadoop-3.1.3/etc/hadoop/workers 

```
hadoop102
hadoop103
hadoop104
```



---

#### Web 端查看 HDFS 的 NameNode 

- 浏览器中输入：http://hadoop102:9870 



#### Web 端查看 YARN 的 ResourceManager 

- 浏览器中输入：http://hadoop103:8088 

