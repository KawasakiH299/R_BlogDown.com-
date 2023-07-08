---
title: Python内置函数
author: Xin Lu
date: '2023-05-04'
slug: []
categories: []
tags: []
---

实例

- enumerate(sequence, [start=0])

```
L = ['Spring', 'Summer', 'Fall', 'Winter']
enumerate(L)
<enumerate at 0x226e1ee1138>#生成的额迭代器，无法直接查看
list(enumerate(L))#列表形式，可以看到内部结构，默认下标从0开始
[(0, 'Spring'), (1, 'Summer'), (2, 'Fall'), (3, 'Winter')]
 
 
list(enumerate(L, start=1)) #下标从 1 开始
[(1, 'Spring'), (2, 'Summer'), (3, 'Fall'), (4, 'Winter')]
 
 
for i,v in enumerate(L):
print(i,v)
0 Spring
1 Summer
2 Fall
3 Winter
 
 
for i,v in enumerate(L,1):
    print(i,v)
1 Spring
2 Summer
3 Fall
4 Winter
 
 
s = ["a","b","c"]
 
 
for i ,v in enumerate(s,2):
print(i,v)
2 a
3 b
4 c
 
 
普通的 for 循环
i = 0
seq = ['one', 'two', 'three']
for element in seq:
print (i, seq[i])
    i+= 1
0 one
1 two
2 three
 
 
在看一个普通循环的对比案例    
for 循环使用 enumerate
 
 
seq = ['one', 'two', 'three']
for i, element in enumerate(seq):
    print (i, element)
0 one
1 two
2 three
 
seq = ['one', 'two', 'three']
for i, element in enumerate(seq,2):
print (i, element)
2 one
3 two
4 three
```

- filter(function, iterable)

```
参数：

function -- 判断函数。

iterable -- 可迭代对象。




fil = filter(lambda x: x>10,[1,11,2,45,7,6,13])
fil
 <filter at 0x28b693b28c8>
list(fil)
[11, 45, 13]
 
 
def is_odd(n):
return n % 2 == 1
 
 
newlist = filter(is_odd, [1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
print(list(newlist))
[1, 3, 5, 7, 9]
```



- **eval()**

**描述：**将字符串str 当成有效的表达式来求值并返回计算结果取出字符串中内容

**语法：**eval(expression[, globals[, locals]])



- **exec()**

  **描述：**执行储存在字符串或文件中的Python语句，相比于eval，exec可以执行更复杂的Python代码。



- **memoryview()**

  **描述：****memoryview()** 函数返回给定参数的内存查看对象(Momory view)。返回由给定实参创建的“内存视图”对象， Python 代码访问一个对象的内部数据，只要该对象支持缓冲区协议 而无需进行拷贝

  **语法：**memoryview(obj)



- **callable()**

  **描述：**callable() 函数用于检查一个对象是否是可调用的。如果返回 True，object 仍然可能调用失败；但如果返回 False，调用对象object绝对不会成功。对于函数、方法、lambda 函式、 类以及实现了 __call__ 方法的类实例, 它都返回True。

```
#检查一个数字
callable(0)
False
 
 
#创建一个函数
def add(x,y):
    return x+y 
callable(add)
True
 
 
#创建一个带有__call__方法的类
class Dogs:
    def __call__(self):
        return 0
callable(Dogs)    
True
```





- **hasattr()**

  **描述：**函数用于判断对象是否包含对应的属性。

  **语法：**hasattr(object, name)

**参数：**

- object -- 对象。
- name -- 字符串，属性名。

```
class Coordinate:
    x = 10
    y = -5
    z = 0
 
 
point1 = Coordinate() 
print(hasattr(point1, 'x'))
True
print(hasattr(point1, 'y'))
True
print(hasattr(point1, 'z'))
True
print(hasattr(point1, 'no'))  # 没有该属性
False
```

