---
title: python线程
author: Xin Lu
date: '2023-05-04'
slug: []
categories: []
tags: []
---

**以下是对发现的几种多线程进行的汇总整理，均已测试运行**
多线程实现的四种方式分别是：
multiprocessing下面有两种：

```
from multiprocessing.dummy import Pool as ThreadPool  # 线程池

from multiprocessing.pool import ThreadPool   # 线程池，用法无区别，唯一区别这个是线程池

```

另外两种：

````
from concurrent.futures import ThreadPoolExecutor  # python原生线程池，这个更主流

import threadpool  # 线程池，需要 pip install threadpool，很早之前的

````

