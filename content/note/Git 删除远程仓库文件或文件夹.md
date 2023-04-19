---
title: Git 删除远程仓库文件或文件夹
author: Xin Lu
date: '2023-04-19'
slug: []
categories: []
tags: []
---

 [前提是本地仓库与远程仓库建立连接的基础上]()

``` 
git remote add origin 仓库地址
```



- 先将远程代码pull到本地，保持本地仓库跟远端仓库同步。

```
git pull
```



- 远程分支 master 上有文件夹 networks，现在不需要了，想删除。

```
git rm -rf networks/
git commit -m "networks is no longer needed"

```

---

- 远程分支 master 上有文件夹 networks，现在不需要了，但本地分支想保留。

```
git rm -rf --cached networks/
git commit -m "networks is no longer needed"

```

- 将修改提交到本地仓库

```
git commit -m '修改信息'
```



- push到远程仓库

```
git push
```

