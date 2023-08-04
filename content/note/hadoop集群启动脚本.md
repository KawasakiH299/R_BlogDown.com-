---
title: 编写hadoop 高可用 shell脚本
author: Xin Lu
date: '2023-08-03'
slug: []
categories: []
tags: []
---



#### 编写hadoop 高可用 shell脚本 

```
vim hastart.sh
```

```
#!/bin/bash

if [ $# -lt 1 ]
then
    echo "No Args Input..."
    exit ;
fi

case $1 in
"start")
        echo " =================== 启动 hadoop集群 ==================="

​```
    echo " --------------- 启动 hdfs ---------------"
    ssh hadoop102 "/opt/ha/hadoop-3.1.3/sbin/start-dfs.sh"
    echo " --------------- 启动 yarn ---------------"
    ssh hadoop103 "/opt/ha/hadoop-3.1.3/sbin/start-yarn.sh"
    echo " --------------- 启动 historyserver ---------------"
    ssh hadoop102 "/opt/ha/hadoop-3.1.3/bin/mapred --daemon start historyserver"
​```

;;
"stop")
        echo " =================== 关闭 hadoop集群 ==================="

​```
    echo " --------------- 关闭 historyserver ---------------"
    ssh hadoop102 "/opt/ha/hadoop-3.1.3/bin/mapred --daemon stop historyserver"
    echo " --------------- 关闭 yarn ---------------"
    ssh hadoop103 "/opt/ha/hadoop-3.1.3/sbin/stop-yarn.sh"
    echo " --------------- 关闭 hdfs ---------------"
    ssh hadoop102 "/opt/ha/hadoop-3.1.3/sbin/stop-dfs.sh"
​```

;;
*)
    echo "Input Args Error..."
;;
esac
```



#### 赋予执行权限

```
chmod +x zk.sh
```