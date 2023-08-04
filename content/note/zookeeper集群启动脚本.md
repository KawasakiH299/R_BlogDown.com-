---
title: 编写zookeeper shell脚本
author: Xin Lu
date: '2023-08-03'
slug: []
categories: []
tags: []
---

#### 编写zookeeper shell脚本 

```
vim zk.sh
```

```shell
#!/bin/bash
case $1 in
"start"){
for i in hadoop102 hadoop103 hadoop104
do
        echo "---------- zookeeper $i 启动 ------------"
        ssh $i "/opt/module/zookeeper-3.5.7/bin/zkServer.sh start"
done
};;
"stop"){
for i in hadoop102 hadoop103 hadoop104
do
        echo "---------- zookeeper $i 停止 ------------"
        ssh $i "/opt/module/zookeeper-3.5.7/bin/zkServer.sh stop"
done
};;
"status"){
for i in hadoop102 hadoop103 hadoop104
do
        echo "---------- zookeeper $i 状态 ------------"
        ssh $i "/opt/module/zookeeper-3.5.7/bin/zkServer.sh status"
done
};;

esac
```



#### 赋予执行权限

```
chmod +x zk.sh
```























