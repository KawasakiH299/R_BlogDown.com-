---
title: numpy  pandas读取文件
author: Xin Lu
date: '2023-04-26'
slug: []
categories: []
tags: []
---



### numpy

#### **np.load()**

```
numpy.load(file, mmap_mode=None, allow_pickle=True, fix_imports=True, encoding=’ASCII’)

```

#### np.save()

```
numpy.save(file, arr, allow_pickle=True, fix_imports=True)。
```



---

### pandas

#### 读取excel

```
import pandas as pd
data = pd.read_excel('path', sheetname = 'sheet1', header = 0, names = ['第一列','第二列','第三列'])
```

path：要读取的文件绝对路径
sheetname：指定读取excel中哪一个工作表，默认sheetname = 0，即默认读取excel中的第一个工作表
若sheetname = ‘sheet1’，即读取excel中的sheet1工作表；
若sheetname = ‘汇总’,即读取excel中命名为“汇总”的工作表；
header：用作列名的行号，默认为header = 0
若header = None，则表明数据中没有列名行；
若header = 0，则表明第一行为列名；
names：列名命名或重命名

---

#### 读取csv

```
import pandas as pd
data = pd.read_csv('path',sep = ',', header = 0, names = ['第一列','第二列','第三列'], encoding = 'utf-8')

```

path：要读取的文件绝对路径
sep：指定列与列间的分隔符，默认sep = ‘,’
若sep = ‘\t’，即列与列间用制表符\t分隔；
若sep = ‘,’，即列与列间用逗号,分隔；
header：用作列名的行号，默认为0
若header = None，则表明数据中没有列名行；
若header = 0，则表明第一行为列名；
names：列名命名或重命名
encoding：指定用于unicode文本编码格式
若encoding = ‘utf-8’，则表明用UTF-8编码的文本；
若encoding = ‘gbk’，则表明用gbk编码的文本；



---

#### 读取txt

pandas中的pd.read_csv即可以读取csv文件，也可以读取txt文件方法同上，也可以用pd.read_table读取txt文件，区别在于sep的默认参数不同。

```
import pandas as pd
data = pd.read_table('path', sep = '\t', header = None, names = ['第一列','第二列','第三列'])

```

path：要读取的文件绝对路径
sep：指定列与列间的分隔符，默认sep = ‘\t’
若sep = ‘\t’，即列与列间用制表符\t分隔；
若sep = ‘,’，即列与列间用逗号,分隔；
header：用作列名的行号，默认为header = 0
若header = None，则表明数据中没有列名行；
若header = 0，则表明第一行为列名；
names：列名命名或重命名
