---
title: hadoop集群完善（非HA）
author: Xin Lu
date: '2023-08-10'
slug: []
categories: []
tags: []
---

### **配置历史服务器** 

为了查看程序的历史运行情况，需要配置一下历史服务器。具

```
 vim mapred-site.xml
 
 
 在该文件里面增加如下配置。


<!-- 历史服务器端地址 -->
<property>
 	<name>mapreduce.jobhistory.address</name>
 	<value>hadoop102:10020</value>
</property>
<!-- 历史服务器 web 端地址 -->
<property>
 	<name>mapreduce.jobhistory.webapp.address</name>
 	<value>hadoop102:19888</value>
</property>
```

#### 启动历史服务器

```
mapred --daemon start historyserver
```

#### Web查看历史服务器

```
http://hadoop102:19888/jobhistory
```



---

### **配置日志的聚集**

日志聚集概念：应用运行完成以后，将程序运行日志信息上传到 HDFS 系统上

```
 vim yarn-site.xml
 
 
 <!-- 开启日志聚集功能 -->
<property>
 	<name>yarn.log-aggregation-enable</name>
 	<value>true</value>
</property>
<!-- 设置日志聚集服务器地址 -->
<property> 
 	<name>yarn.log.server.url</name> 
 	<value>http://hadoop102:19888/jobhistory/logs</value>
</property>
<!-- 设置日志保留时间为 7 天 -->
<property>
 	<name>yarn.log-aggregation.retain-seconds</name>
 	<value>604800</value>
</property>
```



#### Web查看历史服务器

```
http://hadoop102:19888/jobhistory
```

### 集群时间同步

如果服务器在公网环境（能连接外网），可以不采用集群时间同步，因为服务器会定期 

和公网时间进行校准； 

如果服务器在内网环境，必须要配置集群时间同步，否则时间久了，会产生时间偏差， 

导致集群执行任务时间不同步。 

 sudo systemctl status ntpd

 sudo systemctl status ntpd 

 sudo systemctl start ntpd 

 sudo systemctl is-enabled ntpd 



- 修改 hadoop102 的 ntp.conf 配置文件 

[atguigu@hadoop102 ~]$ sudo vim /etc/ntp.conf 

【（授权 192.168.10.0-192.168.10.255 网段上的所有机器可以从这台机器上查 

询和同步时间】

\#restrict 192.168.10.0 mask 255.255.255.0 nomodify notrap 

为 restrict 192.168.10.0 mask 255.255.255.0 nomodify notrap 

（集群在局域网中，不使用其他互联网上的时间） 

server 0.centos.pool.ntp.org iburst 

server 1.centos.pool.ntp.org iburst 

server 2.centos.pool.ntp.org iburst 

server 3.centos.pool.ntp.org iburst 

为 

**#**server 0.centos.pool.ntp.org iburst 

**#**server 1.centos.pool.ntp.org iburst 

**#**server 2.centos.pool.ntp.org iburst 

**#**server 3.centos.pool.ntp.org iburst 

添加 3（当该节点丢失网络连接，依然可以采用本地时间作为时间服务器为集群中 

的其他节点提供时间同步） 

server 127.127.1.0 

fudge 127.127.1.0 stratum 10 



- 修改 hadoop102 的/etc/sysconfig/ntpd 文件 

[atguigu@hadoop102 ~]$ sudo vim /etc/sysconfig/ntpd 

增加内容如下（让硬件时间与系统时间一起同步） 

SYNC_HWCLOCK=yes 



- 重新启动 ntpd 服务 

[atguigu@hadoop102 ~]$ sudo systemctl start ntpd 



- 设置 ntpd 服务开机启动 

[atguigu@hadoop102 ~]$ sudo systemctl enable ntpd 



- 其他机器配置（必须**root** **用户）** 

（1）关闭所有节点上 ntp 服务和自启动 

[atguigu@hadoop103 ~]$ sudo systemctl stop ntpd 

[atguigu@hadoop103 ~]$ sudo systemctl disable ntpd 

[atguigu@hadoop104 ~]$ sudo systemctl stop ntpd 

[atguigu@hadoop104 ~]$ sudo systemctl disable ntpd 



- 在其他机器配置 1 分钟与时间服务器同步一次 

[atguigu@hadoop103 ~]$ sudo crontab -e 

编写定时任务如下： 

*/1 * * * * /usr/sbin/ntpdate hadoop102 



- 修改任意机器时间 

[atguigu@hadoop103 ~]$ sudo date -s "2021-9-11 11:11:11" 

- 1 分钟后查看机器是否与时间服务器同步 

[atguigu@hadoop103 ~]$ sudo date 

----

### 运行mapreduce  的jar包

- 查看hadoop classpath

```
[kiko@hadoop2102 hadoop-3.1.3]$ hadoop classpath
/opt/module/hadoop-3.1.3/etc/hadoop:/opt/module/hadoop-3.1.3/share/hadoop/common/lib/*:/opt/module/hadoop-3.1.3/share/hadoop/common/*:/opt/module/hadoop-3.1.3/share/hadoop/hdfs:/opt/module/hadoop-3.1.3/share/hadoop/hdfs/lib/*:/opt/module/hadoop-3.1.3/share/hadoop/hdfs/*:/opt/module/hadoop-3.1.3/share/hadoop/mapreduce/lib/*:/opt/module/hadoop-3.1.3/share/hadoop/mapreduce/*:/opt/module/hadoop-3.1.3/share/hadoop/yarn:/opt/module/hadoop-3.1.3/share/hadoop/yarn/lib/*:/opt/module/hadoop-3.1.3/share/hadoop/yarn/*
```



需要在mapred-site.xml中添加hadoop classpath输出的内容

```
<property>
<name>yarn.app.mapreduce.am.env</name>
<value>HADOOP_MAPRED_HOME=/opt/module/hadoop-3.1.3/etc/hadoop:/opt/module/hadoop-3.1.3/share/hadoop/common/lib/*:/opt/module/hadoop-3.1.3/share/hadoop/common/*:/opt/module/hadoop-3.1.3/share/hadoop/hdfs:/opt/module/hadoop-3.1.3/share/hadoop/hdfs/lib/*:/opt/module/hadoop-3.1.3/share/hadoop/hdfs/*:/opt/module/hadoop-3.1.3/share/hadoop/mapreduce/lib/*:/opt/module/hadoop-3.1.3/share/hadoop/mapreduce/*:/opt/module/hadoop-3.1.3/share/hadoop/yarn:/opt/module/hadoop-3.1.3/share/hadoop/yarn/lib/*:/opt/module/hadoop-3.1.3/share/hadoop/yarn/*
</value>
</property>
<property>
<name>mapreduce.map.env</name>
<value>HADOOP_MAPRED_HOME=/opt/module/hadoop-3.1.3/etc/hadoop:/opt/module/hadoop-3.1.3/share/hadoop/common/lib/*:/opt/module/hadoop-3.1.3/share/hadoop/common/*:/opt/module/hadoop-3.1.3/share/hadoop/hdfs:/opt/module/hadoop-3.1.3/share/hadoop/hdfs/lib/*:/opt/module/hadoop-3.1.3/share/hadoop/hdfs/*:/opt/module/hadoop-3.1.3/share/hadoop/mapreduce/lib/*:/opt/module/hadoop-3.1.3/share/hadoop/mapreduce/*:/opt/module/hadoop-3.1.3/share/hadoop/yarn:/opt/module/hadoop-3.1.3/share/hadoop/yarn/lib/*:/opt/module/hadoop-3.1.3/share/hadoop/yarn/*
</value>
</property>

<property>
<name>mapreduce.reduce.env</name>
<value>HADOOP_MAPRED_HOME=/opt/module/hadoop-3.1.3/etc/hadoop:/opt/module/hadoop-3.1.3/share/hadoop/common/lib/*:/opt/module/hadoop-3.1.3/share/hadoop/common/*:/opt/module/hadoop-3.1.3/share/hadoop/hdfs:/opt/module/hadoop-3.1.3/share/hadoop/hdfs/lib/*:/opt/module/hadoop-3.1.3/share/hadoop/hdfs/*:/opt/module/hadoop-3.1.3/share/hadoop/mapreduce/lib/*:/opt/module/hadoop-3.1.3/share/hadoop/mapreduce/*:/opt/module/hadoop-3.1.3/share/hadoop/yarn:/opt/module/hadoop-3.1.3/share/hadoop/yarn/lib/*:/opt/module/hadoop-3.1.3/share/hadoop/yarn/*
</value>
</property>

```

