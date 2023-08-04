---
title: xsync分发shell脚本
author: Xin Lu
date: '2023-08-04'
slug: []
categories: []
tags: []
---

#### 编写xsync分发shell脚本

```
vim xsync
```



```
#!/bin/bash
#1. 判断参数个数
if [ $# -lt 1 ]
then
 echo Not Enough Arguement!
 exit;
fi

#2. 遍历集群所有机器
for host in hadoop102 hadoop103 hadoop104
do
 echo ==================== $host ====================
 #3. 遍历所有目录，挨个发送
 for file in $@
 do
	 #4. 判断文件是否存在
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



修改脚本 xsync 具有执行权限
[atguigu@hadoop102 bin]$ chmod +x xsync



将脚本复制到/bin 中，以便全局调用 

[atguigu@hadoop102 bin]$ sudo cp xsync /bin/