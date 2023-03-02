---
title: redis--常用数据类型Hash
author: Xinlu
date: '2023-03-01'
slug: redis--常用数据类型Hash
categories: []
tags: []
---



### hset key field value

- hset user:1001 name tom
- 设置一个key为user:1001，field为name的hash



### hget  key  field

- hget user:1001 name
- 查看key为user:1001field为name的值



### hmset  key1  field1  value1  field2  value2

- hmset  user:1001  id  20220601yy  name  yy
- 给key为user:1001设置多个field和value



### hexists  key1  field 

- hexists  user:1001 name
- 查看key为user:1001的hash是否存在名为name的field



###  hkeys key

- hkeys user:1001
- 列出该hash集合的所有key



### hvals key

- hvals  user:1001 
- 列出该hash集合的所有value



### hincrby  key  field  n（数值）

- hincrby user:1001 age 1
- 给field为age的值加1



### hsetnx   key   field   value

- hsetnx  user:1001 age 10
- 将field的值设置为10 ，且当field不存在时再能执行
