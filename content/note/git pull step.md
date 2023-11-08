
---
title: git pull  stpe
author: Xin Lu
date: '2023-11-08'
slug: []
categories: []
tags: []
---

Kawasaki-Ginlt@Kawasaki-Gin MINGW64 /d/RBlogdown
$ git init
Initialized empty Git repository in D:/RBlogdown/.git/

Kawasaki-Ginlt@Kawasaki-Gin MINGW64 /d/RBlogdown (master)
$ git remote add origin git@github.com:KawasakiH299/R_BlogDown.com-.git

Kawasaki-Ginlt@Kawasaki-Gin MINGW64 /d/RBlogdown (master)
$ git branch -m main

Kawasaki-Ginlt@Kawasaki-Gin MINGW64 /d/RBlogdown (main)
$ git pull --rebase origin main
remote: Enumerating objects: 546, done.
remote: Counting objects: 100% (205/205), done.
remote: Compressing objects: 100% (116/116), done.
remote: Total 546 (delta 112), reused 172 (delta 84), pack-reused 341
Receiving objects: 100% (546/546), 183.77 KiB | 136.00 KiB/s, done.
Resolving deltas: 100% (298/298), done.
From github.com:KawasakiH299/R_BlogDown.com-
 * branch            main       -> FETCH_HEAD
 * [new branch]      main       -> origin/main

Kawasaki-Ginlt@Kawasaki-Gin MINGW64 /d/RBlogdown (main)
$ git status
On branch main
nothing to commit, working tree clean

