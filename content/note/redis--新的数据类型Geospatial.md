---
title: redis--新的数据类型Geospatial
author: Xinlu
date: '2023-03-06'
slug: redis--新的数据类型Geospatial
categories: []
tags: []
---



### 记录经纬度坐标，距离 查询等操作



### geoadd key 经度  纬度  城市名称

- geoadd china：city   12.3  45.6  shanghai
- 添加元素





### geopos  key  城市名称

- geopos  china:city  shanghai
- 查看上海的经纬度





### geodist  key  member1  member2  km/m

- geodist  chian：city   shanghai  beijing  km
- 查看上海到北京的直线距离用km表示





### georadius  key 经度  纬度  半径 km/m

- georadius   china：city  110  20  100 km
- 查看以经度为110纬度为20的圆心100km为半径的内的元素

 
