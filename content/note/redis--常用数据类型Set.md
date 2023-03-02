---
title: redis--常用数据类型Set
author: Xinlu
date: '2023-02-27'
slug: redis--常用数据类型Set
categories: []
tags: []
---



### Set是String类型的无序集合，底层是value为null的hash表，所以添加  查找  删除的复杂度都是O（1）

### 一个算法，随着数据的增加，执行时间的长短，如果是O（1），数据增加，查找数据的时间不变



### sadd  key  value1  value2 value3

- sadd  s1 v1  v2  v3
- 将一个或多个member元素添加到集合key中



### smembers key 

- smembers s1
- 取出该集合的所有值



### ismember key value

- ismember s1  v1
- 判断集合s1中是否存在v1



### scard key

- scard s1
- 返回集合的元素个数



### srem key value1 value2

- srem s1 v1 v2
- 删除集合s1中的v1  v2



### spop  key

- spop s1
- 从s1集合中随机吐出一个元素



### srandmember key n（数量）

- srandmember s1 2
- 从集合s1中随机取出2个元素，不会从集合中删除



### smove set1（移动元素的集合）  set2（目标集合）value

- smove s1 s2 v1
- 将s1集合中的v1移动到s2



### sinter key1  key2 

- sinter  s1  s2
- 返回两个集合的交集元素



### sunion key1  key2 

- sunion s1  s2
- 返回两个集合的并集



### sdiff key1  kdy2

- sdiff  s1  s2
- 返回两个集合的差集
