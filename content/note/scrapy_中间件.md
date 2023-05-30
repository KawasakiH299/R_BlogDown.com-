---
title: scrapy_中间件
author: Xin Lu
date: '2023-04-15'
slug: []
categories: []
tags: []
---

实例

# Downloader Middleware

- 处理request

Downloader Middleware的功能十分强大，修改User-Agent、处理重定向、设置代理、失败重试、设置Cookies等功能都需要借助它来实现。下面我们来了解一下Downloader Middleware的详细用法。

- 处理response

- ```
  每个Downloader Middleware都定义了一个或多个方法的类，核心的方法有如下三个。
  
  process_request(request, spider)。
  process_response(request, response, spider)。
  process_exception(request, exception, spider)
  ```

---

# Spider Middleware

- 处理item

  ```
  每个Spider Middleware都定义了以下一个或多个方法的类，核心方法有如下4个。
  
  process_spider_input(response, spider)。
  process_spider_output(response, result, spider)。
  process_spider_exception(response, exception, spider)。
  process_start_requests(start_requests, spider)。
  
  
  ```

只需要实现其中一个方法就可以定义一个 Spider Middleware。下面我们来看看这4个方法的详细用法。

## 1. process_spider_input(response, spider)

当Response被Spider Middleware处理时，`process_spider_input()`方法被调用。 

`process_spider_input()`方法的参数有如下两个。

- `response`，是Response对象，即被处理的Response。
- `spider`，是Spider对象，即该Response对应的Spider。

`process_spider_input()`应该返回None或者抛出一个异常。

- 如果它返回None，Scrapy将会继续处理该Response，调用所有其他的Spider Middleware，直到Spider处理该Response。
- 如果它抛出一个异常，Scrapy将不会调用任何其他Spider Middleware的`process_spider_input()`方法，而调用Request的`errback()`方法。`errback`的输出将会被重新输入到[中间件](https://cloud.tencent.com/product/tdmq?from=20065&from_column=20065)中，使用`process_spider_output()`方法来处理，当其抛出异常时则调用`process_spider_exception()`来处理。

## 2. process_spider_output(response, result, spider)

当Spider处理Response返回结果时，`process_spider_output()`方法被调用。 

`process_spider_output()`方法的参数有如下三个。

- `response`，是Response对象，即生成该输出的Response。
- `result`，包含Request或Item对象的可迭代对象，即Spider返回的结果。
- `spider`，是Spider对象，即其结果对应的Spider。

`process_spider_output()`必须返回包含Request或Item对象的可迭代对象。

## 3. process_spider_exception(response, exception, spider) 

当Spider或Spider Middleware的`process_spider_input()`方法抛出异常时，`process_spider_exception()`方法被调用。 

`process_spider_exception()`方法的参数有如下三个。

- `response`，是Response对象，即异常被抛出时被处理的Response。
- `exception`，是Exception对象，即被抛出的异常。
- `spider`，是Spider对象，即抛出该异常的Spider。

`process_spider_exception()`必须要么返回`None`，要么返回一个包含Response或Item对象的可迭代对象。

- 如果它返回`None`，Scrapy将继续处理该异常，调用其他Spider Middleware中的`process_spider_exception()`方法，直到所有Spider Middleware都被调用。
- 如果它返回一个可迭代对象，则其他Spider Middleware的`process_spider_output()`方法被调用，其他的`process_spider_exception()`不会被调用。

## 4. process_start_requests(start_requests, spider)

`process_start_requests()`方法以Spider启动的Request为参数被调用，执行的过程类似于`process_spider_output()`，只不过它没有相关联的Response，并且必须返回Request。

`process_start_requests()`方法的参数有如下两个。

- `start_requests`，是包含Request的可迭代对象，即Start Requests。
- `spider`，是Spider对象，即Start Requests所属的Spider。

`process_start_requests()`必须返回另一个包含Request对象的可迭代对象

---

#### 自定义proxy

```
class HttpbinProxyMiddleware(object):

    logger = logging.getLogger(__name__)

 

    # def process_request(self, request, spider):

    #     # pro_addr = requests.get('http://127.0.0.1:5000/get').text

    #     # request.meta['proxy'] = 'http://' + pro_addr

    #     pass

    #

    # def process_response(self, request, response, spider):

    #     # 可以拿到下载完的response内容，然后对下载完的内容进行修改（修改文本的编码格式等操作）

    #     pass

 

    def process_exception(self, request, response, spider):

        self.logger.debug('Try Exception time')

        self.logger.debug('Try second time')

        proxy_addr = requests.get('http://127.0.0.1:5000/get').text

        self.logger.debug(proxy_addr)

        request.meta['proxy'] = 'http://{0}'.format(proxy_addr)
```

