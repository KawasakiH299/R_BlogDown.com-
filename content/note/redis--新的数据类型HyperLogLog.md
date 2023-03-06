---
title: redis--新的数据类型HyperLogLog
author: Xinlu
date: '2023-03-06'
slug: redis--新的数据类型HyperLogLog
categories: []
tags: []
---



### 主要用于解决基数问题，可以做到去重



### pfadd key  value

- pfadd  program  “java”
- pfadd  program  “redis”  “C++”
- pfadd  program  “java”

- 向programe中添加元素，但java元素只能存在一次







### pfcount key （key）

- pfcount programe 
- 查询programe中有几个基本元素







### pfmerge  

- pfmerge  programe_all  programe1  programe2

- 将programe1和programe2中的元素合并添加到programe_all中去

