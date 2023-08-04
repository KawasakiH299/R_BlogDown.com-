---
title: linux主机准备
author: Xin Lu
date: '2023-08-04'
slug: []
categories: []
tags: []
---

#### 配置网络

```
[root@hadoop102 ~]# cat /etc/sysconfig/network-scripts/ifcfg-ens33
TYPE="Ethernet"
PROXY_METHOD="none"
BROWSER_ONLY="no"
BOOTPROTO="static"
DEFROUTE="yes"
IPV4_FAILURE_FATAL="no"
IPV6INIT="yes"
IPV6_AUTOCONF="yes"
IPV6_DEFROUTE="yes"
IPV6_FAILURE_FATAL="no"
IPV6_ADDR_GEN_MODE="stable-privacy"
NAME="ens33"
UUID="206e5e6f-0b43-4991-88ec-57c93e914ac7"
DEVICE="ens33"
ONBOOT="yes"

IPADDR=192.168.121.146
NETMAS=255.255.255.0
GATEWAY=192.168.121.2
DNS1=114.114.114.114

```



#### 修改主机名

```
[root@hadoop100 ~]# vim /etc/hostname
hadoop102
```



#### 添加本地NDS解析

```
[root@hadoop100 ~]# vim /etc/hosts
添加如下内容
192.168.10.100 hadoop100
192.168.10.101 hadoop101
192.168.10.102 hadoop102
192.168.10.103 hadoop103
192.168.10.104 hadoop104
```

