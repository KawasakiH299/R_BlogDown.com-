---
title: git push stpe
author: Xin Lu
date: '2023-11-08'
slug: []
categories: []
tags: []
---

Kawasaki-Ginlt@Kawasaki-Gin MINGW64 /d/Projects/Python-project

$ git init
Initialized empty Git repository in D:/Projects/Python-projects/Data/.git/

Kawasaki-Ginlt@Kawasaki-Gin MINGW64 /d/Projects/Python-projects/Data (master)
$ git branch -m main

Kawasaki-Ginlt@Kawasaki-Gin MINGW64 /d/Projects/Python-projects/Data (main)
$ git remote add origin git@github.com:KawasakiH299/Data-Structure.git
Kawasaki-Ginlt@Kawasaki-Gin MINGW64 /d/Projects/Python-projects/Data (main)
$ git add .

Kawasaki-Ginlt@Kawasaki-Gin MINGW64 /d/Projects/Python-projects/Data (main)
$ git commit -m 'version:1.0'
[main (root-commit) 3316c0e] version:1.0
 5 files changed, 251 insertions(+)
 create mode 100644 "\345\215\225\351\223\276\350\241\250/README"
 create mode 100644 "\345\215\225\351\223\276\350\241\250/SingleList.py"
 create mode 100644 "\345\215\225\351\223\276\350\241\250/__init__.py"
 create mode 100644 "\345\215\225\351\223\276\350\241\250/demon02.py"
 create mode 100644 "\345\215\225\351\223\276\350\241\250/test.py"

Kawasaki-Ginlt@Kawasaki-Gin MINGW64 /d/Projects/Python-projects/Data (main)
$ git pull --rebase origin main
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), 604 bytes | 35.00 KiB/s, done.
From github.com:KawasakiH299/Data-Structure
 * branch            main       -> FETCH_HEAD
 * [new branch]      main       -> origin/main
Successfully rebased and updated refs/heads/main.

Kawasaki-Ginlt@Kawasaki-Gin MINGW64 /d/Projects/Python-projects/Data (main)
$ git push -u origin main
Enumerating objects: 9, done.
Counting objects: 100% (9/9), done.
Delta compression using up to 8 threads
Compressing objects: 100% (6/6), done.
Writing objects: 100% (8/8), 2.64 KiB | 2.64 MiB/s, done.
Total 8 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:KawasakiH299/Data-Structure.git
   536b7eb..c046477  main -> main
branch 'main' set up to track 'origin/main'.



重命名本地分支
git branch -m new_branch_name
当不在当前分支时
git branch -m old_branch_name new_branch_name


ssh -T git@github.com 对ssh key 进行验证：
$ ssh -T git@github.com
Hi xxxx! You've successfully authenticated, but GitHub does not provide shell access.
git@github.com:xxxx.git
