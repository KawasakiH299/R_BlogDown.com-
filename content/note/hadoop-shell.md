---
title: Hadoop  shell script
author: Xin Lu
date: '2022-10-13'
slug: hadoop集群脚本
categories: []
tags: []
---

**1.分发文件脚本！！**                                                

创建一个xsync.sh的文件，将以下shell代码写入文件，并将权限改为可执行文件权限即可。
```#!/bin/bash
#1. 判断参数个数                                                
if [ $# -lt 1 ]                                                   
then
  echo Not Enough Arguement!
  exit;
fi
#2. 遍历集群所有机器
for host in hadoop102 hadoop103 hadoop104
do
  echo ====================  $host  ====================
  #3. 遍历所有目录，挨个发送
  for file in $@
  do
    #4 判断文件是否存在
    if [ -e $file ]
    then
      #5. 获取父目录
      pdir=$(cd -P $(dirname $file); pwd)
      #6. 获取当前文件的名称
      fname=$(basename $file)
      ssh $host "mkdir -p $pdir"
      rsync -av $pdir/$fname $host:$pdir
    else
      echo $file does not exists!
    fi
  done
done
```
**2.服务器进程脚本！！**

创建一个名为jpsall.sh的文件，将以下shell代码写入文件，并将权限改为可执行文件权限即可。
```# !/bin/bash<
for host in hadoop102 hadoop103 hadoop104
do
        echo=============== $host ===============
        ssh $host jps
done
```


**3.ZOOKEEPER启动   关闭  查看状态！！**

创建一个zk.sh的文件，将以下shell代码写入文件，并将权限改为可执行文件权限即可。
启动命令zk.sh start
关闭命令zk.sh stop
```

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
**本文为CSDN博主「川崎H2车主」的原创文章[详细请见](https://blog.csdn.net/qq_44641456/article/details/124619714)**
