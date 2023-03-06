---
title: redis--常用数据类型List
author: Xinlu
date: '2023-02-27'
slug: redis--常用数据类型List
categories: []
tags: []
---



### List底层是双向链表，可插入首部或尾部，对两端操作性能高，中间通过索引操作



### lpush/rpush  key  value1 value2 value3

- lpush L1 v1 v2 v3
- 从左/右加入value值v1  v2  v3
- 从左边放入的，被后放入的挤到右边
- 从右边放入的，被后放入的挤到左边



### lpop/rpop key

- lpop L1
- 吐出最左/右边的值，吐出后就不存在了



### rpoplpush key1 key2

- rpoplpush  L1  L2
- 从l1最右边的值取出，加入到l2最左边



### lrange key  start stop

- lrange L1 0  -1
- 按照索引下标获取元素



### lindex  key  index

- lindex  L1  3
- 按照索引下标获得元素



### llen key

- llen L1
- 获得列表长度



### linset  key  before  列表中有的值  value

- linset L1 before “ 列表中有的值 ”  “value_new”



### lrem key  数量（n） value

- 从左边删除n个value的值



### lset key index（索引） value

- lset L1 1 abc
- 为L1更新索引为1的值

### BLPOP list1 100
- 操作会被阻塞，如果指定的列表 key list1 存在数据则会返回第一个元素，否则在等待100秒后会返回 nil 。
