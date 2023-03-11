---
title: redis--常用数据类型Zset
author: Xinlu
date: '2023-03-01'
slug: redis--常用数据类型Zset
categories: []
tags: []
---



## 有序集合Zset：主要用于数值的排名

###  是一个没有重复元素的字符串集合

### 于set的不同之处时有序集合Zset的每个成员都关联了一个评分（score），这个评分被用来按照从最低分到最高峰的方式排序集合中的成员，集合的成员时唯一的但评分可以是重复的



### zadd key  score1 value1 score2  value2

- zadd  top  200  python  300  c++  400  java
- 将一个或多个member元素及其score值加入到有序集合



### zrange  key  start stop  (withscores)

- zrange top 0 -1 （withscores）
- 取出0到-1的value值（和score的值）


### zscore key  value
- zscore z1 java
- 获取java的scores值 


### zrangebyscore  key  min   max （withscores）

- zrangebyscore top   200  400
- 取出score为200到400的value值，从小到大依次排序



### zrevrangebyscore  key  max   min（withscores）

- zrangebyscore top   400  200
- 取出score为400到200的value值，从大到小依次排序



### zincrby  key  n（数值） value

- zincrby  top  50  java
- 给java的score加50



### zrem key value

- zrem top java

- 删除java



### zcount  key  min  max

- zcount  top 100  300
- 统计在分数区间的元素个数



### zrank key  value

- zrank top java
- 返回java在top中的排名





## 案例：用Zset实现一个文章访问量的排行榜

