---
title: HDFS的master节点状态为Standby解决方案
author: Xin Lu
date: '2023-08-04'
slug: []
categories: []
tags: []
---

#### HDFS的master节点状态为Standby解决方案

##### 更改节点状态

```
# 查看namenode节点的HA状态
[root@master ~]# hdfs haadmin -getServiceState nn1
standby
[root@master ~]# hdfs haadmin -getServiceState nn2
active
# 修改nn2为standby状态
[root@master ~]# hdfs haadmin -transitionToStandby --forcemanual nn2
# 修改nn1为active状态
[root@master ~]# hdfs haadmin -transitionToActive --forcemanual nn1
```

##### 查看节点状态

```
[root@master ~]# hdfs haadmin -getServiceState nn1
active
[root@master ~]# hdfs haadmin -getServiceState nn2
standby
```

