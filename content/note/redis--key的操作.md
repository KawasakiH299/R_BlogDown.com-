---
title: redis--key的操作命令
author: Xinlu
date: '2023-02-27'
slug: redis--key的操作命令
categories: []
tags: []
---



### keys *

- 查看当前库所有的key



### exists k1

- 判断k1是否存在



### type k1

- 查看k1是什么类型数据



### del k1

- 删除k1



### unlink k1

- 异步删除k1，先给你显示已经删除，后慢慢删除



### expire k1 10

- 为k1设置10秒过期时间



### ttl k1

- 查看还有多少秒过期，-1表示永不过期，-2表示已经过期



### select 15

- 命令切换数据库，0--15共16个数据库，0号数据库为默认数据库



### dbsize

- 查看当前数据库key的数量



### flushdb 

- 清空当前数据库



### flushall

- 通杀所有数据库