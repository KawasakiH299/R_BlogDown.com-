---
title: Git 分支和tag
author: Xin Lu
date: '2023-04-19'
slug: []
categories: []
tags: []
---

实例

#### 查看本地分支

````
$ git brach
````

#### **查看远程分支**

```
$ git branch -r
```

#### **查看所有分支**

```
git branch -a
```

#### **创建本地新分支**

```
git branch [branch name]
```

#### **切换到新分支**

- 在新的分支下即可操作改分支的内容
- 保持与远程仓库同步：git pull【`git pull`是在提交到远程仓库之前，先更新到最新版本代码，防止和别人代码产生冲突。】

```
git checkout [branch name]
```

#### 推送不同分支到远程

```
git push origin [branch name]
git push origin main
```

#### 删除本地分支

```
git branch -d [branch name]
```

#### **删除远程分支**

```
git push origin –delete :[branch name]
```







#### 推送本地新分支到远程仓库**(前提是与远程仓库连接并同步)

```
git push origin [branch name]:[branch name]
```

【与远程仓库连接：git remote add origin 仓库地址（ssh）】

【与远程仓库同步：git pull】



#### tag是代码版本控制的标签

- tag 对应某次 commit



#### 查看commit的hash

```
$ git log --oneline

$ git tag -l "v1" 
// 加上参数 -l 可以使用通配符来过滤 tag
```





#### 打 tag 不需要在 HEAD 之上，也可以在某次历史提交上打（通过 `git log` 获取之前的提交记录commit-id）

```
$ git tag -a v3.0 ff28fd51 -m "给之前的提交记录打tag" 
```



#### 切换tag版本

```
git checkout tag_name 
```

