---
title: redis--常用数据类型String
author: Xinlu
date: '2023-02-27'
slug: redis--常用数据类型String
categories: []
tags: []
---





### String 可以存图片，value值最大可存512M



### set  key  value

- set k1 v1
- 设置k1的value为v1，set可以被新值覆盖set k1 v2



### get   key

- get k1
- 查询k1的value值



### setnx  key  value

- setnx k2 v2
- 只有当key不存在时，才能设置，不能被覆盖



### append key value

- append k1 abc
- 将给定的value值追加到原值的末尾，返回值的长度



### strlen key

- strlen k1
- 查看k1的长度



### incr  key 

- incr k1
- 将k1中的值加1



### decr  key

- decr k1
- 将k1中的值减1



### redis是单线程，redis操作时原子性的，每个操作都是一个线程，原子性操作是不会被线程调度机制打断的

### redis是单线程加多路I/O复用





### incrby  key  步长

- incrby k1 20
- 给k1加20



### decrby key 步长

- decrby k1 20
- 将k1减20



### mset key1 value1 key2 value2

- mset k1 v1 k2 v2
- 同时设置多个key-value



### mget key1 value1 key2 value2

- mget k1 k2
- 同时获取多个key的值



### msetnx  key1 value1 key2 value2

- msetnx k1 v1 k2 v2
- 同时设置多个key-value，当且仅当所有key不存在时



### getrange key 开始位置  结束位置

- getrange name 0 3
- 可以取到位置0和位置3



### setrange key 起始位置 value

- 从给定的起始位置开始，用value值覆盖原先的值，索引位置从0开始
- setrange k1 2 abcd



### setex  key 过期时间 value

- setex k1 10 v1
- 设置过期时间



### getset key value

- getset k1 new
- 给k1设置新值，返回旧值