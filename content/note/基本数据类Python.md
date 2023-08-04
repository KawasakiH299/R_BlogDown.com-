---
title: 名字绑定
author: Xin Lu
date: '2023-05-31'
slug: []
categories: []
tags: []
---


#### int数据类型内存池

- 整型作为最常用的,频繁参与计算的数据类型，在python3.5中解释器会自动在内存中创建-5-3000之间的

- bool型继承了int型，他是int的子类。

- Python2中有长整型long，数值范围更大，在python3中已取消，所有整型统一由int表示

#### python整数和[浮点型](https://so.csdn.net/so/search?q=浮点型&spm=1001.2101.3001.7020)支持常规的数值运算

- 整数和浮点数都可参与的运算：+  -  *  /  %（取余）  //（整除）  **（幂）

#### Python 数据类型

```
 1. 数字 Number
 2. 字符串 String 
 3. 列表 List 
 4. 元组 Tuple 
 5. 字典 Dict 
 6. 集合 Set 

其中 数字 Number 和 字符串 String 是基本的数据类型
其中 数字 Number 和 字符串 String 与 元组 Tuple 是不可变数据类型
其中 列表 List 和 字典 Dictionary 与 集合 Set 是可变数据类型

其中 字符串 String 和 列表 List 与 元组 Tuple 是可偏移量索引数据类型
其中 字典 Dictionary 是可键值索引数据类型
其中 集合 Set 是不可索引数据类型
```

#### **Python 中有三类主要的数据结构**

```
 1，序列 
 字符串 String 
 列表 List 
 元组 Tuple 

 2，散列 
 字典 Dict 

 3，集合 
 集合 Set 

# 二进制
var = bin(22)
# Out: '0b10110'
# 八进制
var = oct(22)
# Out: '0o26'
# 十六进制
var = hex(22)
# Out: '0x16'

var = complex(2, 2)
# Out: 2 + 2j
```

#### 字符串

```
'''
# 默认转义
\\ 反斜杠符号(\)
\' 单引号
\" 双引号
# ASCII码特殊字符
\a 响铃
\b 退格(backspace)
\n 换行
\v 纵向制表符
\t 横向制表符
\r 回车
\f 换页
'''

```

方法

```
strip() 方法用于移除字符串头尾指定的字符（默认为空格或换行符）或字符序列。

注意：该方法只能删除开头或是结尾的字符，不能删除中间部分的字符。
```



#### 元组

创建

```
# 直接定义元组，必须包含一个逗号，若元组是更大表达式中的一部分则必须包含圆括号，元组是一个「不变」的列表，一旦创建其中各个元素的地址便不能改变
var = ('wh', 'zl', 'yzh', 'zhb', 666) 
var = 'wh', 'zl', 'yzh', 'zhb', 666 
var = (666,)
# 生成式，最多输入一个参数，可以是任意六种标准数据类型
var = tuple('argument')

```

访问

```
# 访问元组中元素，与访问列表变量类似可以索引、切片与判存

```

增删改查

```
# 元组没有增、删、改的方法但是可以查询；可以改变元组中的可变对象的元素从而实现间接改变元祖元素
var.index("wh")
var.count("wh")
# 可以组合元组
var1 + var2
# 重复元组 n 次
var1 * n

```



#### 列表

##### 定义

```
# 直接定义列表
var = ['wh', 'zl', 'yzh', 'zhb', 666]


# 生成式，最多输入一个参数，可以是任意六种标准数据类型
>>> var = list('argument')
>>> var
['a', 'r', 'g', 'u', 'm', 'e', 'n', 't']


# 推导式，可从左往右嵌套使用 for 与 if，使用 () 包裹返回列表生成器，而使用 [] 包裹将得到列表 
>>> var1 = [i2 for i1 in [[1,2],[3,4]] for i2 in i1]
>>> var1
[1, 2, 3, 4]
>>> var2 = [i2 for i1 in [[1,2],[3,4]] for i2 in i1 if i2 %2 ==0]
>>> var2
[2, 4]

```

##### 访问

```
>>> var = ['wh','zl','yzh']
>>> var[2]
'yzh'


>>> var[0:-1:2]
['wh']

列表倒叙
>>> var[::-1]
['yzh', 'zl', 'wh']

>>> 'wh' in var
True

```

##### 则删改查

```
取反
>>> var.reverse()
>>> var
['yzh', 'zl', 'wh']

列表相加
>>> var1 = [1,2,3]
>>> var2 = [4,5,6]
>>> var = var1 + var2
>>> var
[1, 2, 3, 4, 5, 6]

重复列表 n 次
>>> var3 = var1 * 3
>>> var3
[1, 2, 3, 1, 2, 3, 1, 2, 3]

列表末尾添加可迭代对象，将其中的元素逐个加入列表中
>>> var1.extend(var2)
>>> var1
[1, 2, 3, 4, 5, 6]


删除列表中第一个匹配元素
>>> var1.remove(1)
>>> var1
[2, 3, 4, 5, 6]


移除列表指定下标处的元素（默认移除最后一个元素），并作为返回值
>>> var1_p = var1.pop(4)
>>> var1_p
6

清除列表
>>> var1.clear()
>>> var1
[]
```

##### 字典

有序字典OrderedDict与dict的区别

```
与Dict区别

常规的Dict被设计为非常擅长映射操作。 跟踪插入顺序是次要的
OrderedDict旨在擅长重新排序操作。 空间效率、迭代速度和更新操作的性能是次要的
OrderedDict在频繁的重排任务中还是比Dict更好，这使他更适用于实现各种 LRU 缓存
OrderedDict类的 popitem() 方法有不同的签名。它接受一个可选参数来指定弹出哪个元素

```

创建

```
# 直接定义字典
var = {'wh':22, 'zl':22, 'yzh':22, 'zhb':22, 211:666, ('针不戳','又拉了'):'那可不'} 
# 生成式, 键与值可以是字符串，数字，元组，其中建必须唯一且可哈希的对象
var = dict('key' = 'value')
# 推导式，使用 {} 包裹 for 与 if 得到字典，可便捷反换 value 与 key 间位置 
var = {key: value for key, value in zip(list1, list2) if value > number}
var = {value: key for key, value in dict.items()}
var = {diction[key]: key for key in diction}

```

访问

```
# 访问字典中元素，通过键索引返回值，不存在将报错
var['wh'] 
# Out: 22
# 访问字典键是否存在，存在返回 True 不存在返回 False
'wh' in var 
# Out: True
# 访问字典中元素，通过键索引返回值，不存则返回 None
var.get('hm') 
# Out: None
# 访问字典中元素，通过键索引返回值，不存则返回 None，并把当前键值写入字典
var.setdefault('hm') 
>>> dic1.setdefault('1')
>>> dic1
{1: 4, 2: 5, 3: 6, '1': None}

```

则删改查

```
# 增加字典元素，可通过不存在的键索引添加或者已存在的键索引修改或使用字典方法
var['wyq'] = 22
var = {'wh':22, 'zl':22, 'yzh':22, 'zhb':22, 211:666, ('针不戳','又拉了'):'那可不', 'wyq':22}
# 删除字典中元素
del var["wh"]
var.clear()
var.popitem()#3.6之后默认有序字典
>>> dic1.popitem()
('1', None)
# 查找字典中元素
var["wh"]
# 修改字典中元素
var["wh"] = 66
# 返回键
var.keys()
# 返回值
var.values()
# 转换为可遍历的字典项目项目对象
var.items()
# 键值对个数
len(var)

```

##### 集合

创建

```
# 直接定义集合
var = {'wh', 'zl', 'yzh', 'zhb', 666} 
# 生成式，最多输入一个参数，可以是任意六种标准数据类型
var = set(argument)
# 推导式，使用 {} 包裹 for 与 if 生成，自动去除重复元素
var = {abs(x) for x in [1, -1, 0, 2, -2] if x != 0}

```

访问

```
集合的元素无序，通过序号索引访问不被允许，集合是可迭代的，for 可遍历访问，可以通过 in 判断元素是否存在，可转换为列表而间接访问
```

则删改查

```
# 添加元素
var.add(item)
# 必须添加可迭代对象，将其中的元素逐个加入集合中
var.updata(item)
# 删除元素
var.remove(item)
# 存在则删除元素
var.discard(item)
# 元素出栈
var.pop()
# 清空
var.claer()
# 浅拷贝
var.copy()
# 交集
var1 & var2
var1.intersection(var2)
# 并集
var1 ｜ var2
var1.union(var2)
# 差集，找出前集合而后集合无的元素
var1 - var2
var1.difference(var2)
# 对称差分集，找出不同属于两个集合的元素
var1 ^ var2
var1.symmetric_difference(var2)
# 子集
var1 < var2
var1.issubset(var2)
# 超集
var1 >= var2
var1.issuperset(var2)
# 两个集合是否不包含相同元素
var1.isdisjoint(var2)

```

#### 深浅拷贝

- 浅拷贝

```
浅拷贝 a={1:[1,2,3]} b=a.copy() 表面上 a 与 b 都是指向独立的对象（a 与 b 的地址不同），但是内部的子对象中的可变元素仍指向同一地址
```

- 深拷贝

````
深拷贝 a={1:[1,2,3]} b=copy.deepcopy(a) 此时 a 与 b 是两个完全独立的对象
````