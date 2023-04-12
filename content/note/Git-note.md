---
title: Git-note
author: Xin Lu
date: '2023-04-02'
slug: Git-note
categories: []
tags: []
---



#### git版本管理

- 目的：
  - 协同多人开发
  - 更新代码版本，同时不删除之前的版本

---



### 国内镜像：http://npm.taobao.org/mirrors/git-for-windows/



---



### 操作界面

- GUI：图形化界面
- BUSH：linux操作

- CMD：win操作



---



### 常用linux命令

1）、cd : 改变目录。

2）、cd . . 回退到上一个目录，直接cd进入默认目录

3）、pwd : 显示当前所在的目录路径。

4）、ls(ll):  都是列出当前目录中的所有文件，只不过ll(两个ll)列出的内容更为详细。

5）、touch : 新建一个文件 如 touch index.js 就会在当前目录下新建一个index.js文件。

6）、rm:  删除一个文件, rm index.js 就会把index.js文件删除。

7）、mkdir:  新建一个目录,就是新建一个文件夹。

8）、rm -r :  删除一个文件夹, rm -r src 删除src目录

9）、mv 移动文件, mv index.html src index.html 是我们要移动的文件, src 是目标文件夹,当然, 这样写,必须保证文件和目标文件夹在同一目录下。

10）、reset 重新初始化终端/清屏。

11）、clear 清屏。

12）、history 查看命令历史。

13）、help 帮助。

14）、exit 退出。

15）、#表示注释



---



### Git中不同颜色的表示

- 蓝色的表示目录
- 白色的表示文件
- 绿色的表示程序



---



### 查看Git的配置

- 用户自己的配置：
  -  git config --global --list
- 系统的配置：
  - git config --system --list



---



### 配置自己的标识（安装后必须要配置的）

- 配置自己的名称
  - git config --global user.name "kawasaki-Ginlt"
- 配置邮箱
  - git config --global user.email 908528125@qq.com



---



### Git的四个目录

- 工作区（Workspace）：在本地写项目代码的路径
  - 将工作区的临时改变的放入暂存区
    - git add  .
    - (.）代表所有文件
- 暂存区（Stage）：只是一些文件，保存临时改动的信息- 
  - 将暂存区的代码放入仓库区
    - git commit
- 仓库区（Respository）：本地存放完整项目的
  - 仓库区推入远程
    - git push
- 远程仓库（Remote）：存放代码的服务器
- .git：存放Git管理信息的目录，初始化仓库的时候自动创建

- Stash：隐藏，是一个工作状态保存栈，用于保存/恢复WorkSpace中的临时状态。



---



### 本地仓库搭建

- git init



---



### 克隆远程仓库

- git clone [url]



---



### Git文件操作

> 版本控制就是对文件的状态进行更新，首先需要知道文件的状态，首先得跟踪文件(untracked)
>
> git管理的文件有三种状态：已修改（modified）,已暂存（staged）,已提交(committed)

- 跟踪文件  git add .  （即提交到暂存区）

- 查看状态  git status

  *git commit -m*

```
#查看指定文件状态git status [filename]#查看所有文件状态
git status# git add .                  添加所有文件到暂存区# 
git commit -m "消息内容"    提交暂存区中的内容到本地仓库 -m 提交信息
```



- 不想上传一些文件，可写一个配置来记录忽略文件，在主目录下建立".gitignore"文件，此文件有如下规则：

```

#为注释
*.txt        #忽略所有 .txt结尾的文件,这样的话上传就不会被选中！
!lib.txt     #但lib.txt除外
/temp        #仅忽略项目根目录下的TODO文件,不包括其它目录temp
build/       #忽略build/目录下的所有文件
doc/*.txt    #会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
```



---



###  生成ssh密钥

- ssh-keygen -t rsa （参数是指定加密算法）

- 在win账户目录下可以查看到xx.pub



---



### Git 分支

- 分支并行执行时，可存在多个版本
- 分支有交集时，可选择保存那个版本
- git分支中常用指令：

```
# 列出所有本地分支
git branch

# 列出所有远程分支
git branch -r

# 新建一个分支，但依然停留在当前分支
git branch [branch-name]

# 新建一个分支，并切换到该分支
git checkout -b [branch]

# 合并指定分支到当前分支
$ git merge [branch]

# 删除分支
$ git branch -d [branch-name]

# 删除远程分支
$ git push origin --delete [branch-name]
$ git branch -dr [remote/branch]
```



- master：为主分支



---



### 版本切换

- 首先查看提交日志
  - git log
  - 从日志中找到需要的版本号

``` commit a3f6a900663f5dfd0875343f508639e0b2cde5a6 (HEAD -> master)
commit a3f6a900663f5dfd0875343f508639e0b2cde5a6 (HEAD -> master)
```

- 选择版本
  - git reset [commit_id]  版本号
    - --mixed (默认选项)
    - --soft
    - --hard



- --mixed参数的变化情况是：
  - 1，版本指针head和分支尖端指针指向我们指定的版本
  - 2，暂存区指针index指向我们指定的版本
  - 3，工作区的内容保持不变



- --soft参数的变化情况是：
  - 1，版本指针head和分支尖端指针指向我们指定的版本
  - 2，暂存区指针index保持不变
  - 3，工作区的内容保持不变



- --hard参数的变化情况是：
  - 1，版本指针head和分支尖端指针指向我们指定的版本
  - 2，暂存区指针index指向我们指定的版本
  - 3，将工作区的内容重置为暂存区的内容



最新版本不会被删除

- 可通过查看切换之前的版本
  - git reflog 
  - git  reset --hard 版本号



- 文件修改的内容也能被记录

## 想要版本切换必须先进暂存区在进本地仓库



### 将本地仓库的代码推送到远程仓库

- 与远程仓库建立连接

```
>>>git remote add origin 仓库地址
```

- 若报错

```
fatal:remote origin already exists

## 报错原因：
##已经将一个远程仓库添加并命名为origin了，所以现在你是在尝试将另一个远程仓库添加并命名为origin，##显然这是一个错误，一个origin不能指向两个仓库

## 解决办法：
## 使用set-url修改origin仓库的url
>>>git remote set-url origin 新的远程仓库链接
## 先将已经添加过的，命名为origin的远程仓库给删了，然后重新添加
>>>git remote rm origin
>>>git remote add origin 新的远程仓库链接
```

- 将当前代码的master分支上传到gitee远程仓库

```
# 不加这句可能报错，原因是 gitee 中的 README.md 文件不在本地仓库中。
# 可以通过该命令进行代码合并
>>>git pull --rebase origin master
>>>git push -u origin master
###第一次上传可能会让输入命令
```

