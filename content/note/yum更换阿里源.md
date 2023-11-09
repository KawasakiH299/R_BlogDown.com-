---
title: yum 通过网络更换yum源
author: Xin Lu
date: '2023-11-09'
slug: []
categories: []
tags: []
---

1、yum源配置（网络）：

1.1先备份原有的yum源：

1 [root@localhost ~]# mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.back
1.2下载新的yum源（阿里）：

1 wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
2 或者
3 curl -o /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
1.3清除原有yum缓存：

1 [root@localhost ~]# yum clean all
1.4生成新的缓存：

1 [root@localhost ~]# yum makecache