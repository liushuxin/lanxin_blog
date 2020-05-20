---
title: Git常用方法
date: 2020-04-14 12:49:58
categories:
  - Git
tags:
  - Git基础
---

## 非常规命令

在实际的工作过程中我们往往会用到一些 git 命令，但是我们时长很难记住他们，这里就做下总结记录，便于以后快速查阅

1. git cherry-pick commitId
   利用 git log 查看要合并的提交 commitId 然后
   利用这个命令来合并

2) 在历史的迭代中，我们有可能把一些文件加入 git 版本跟踪，但是发现不需要，那么我们应该怎么去除跟踪呢？

```git
git rm -r --cached .
git add .
git commit -m '清楚永远不想跟踪的文件'

```

3、清除在线上已经删除的分支信息，而在本地的缓存

```git
git remote update origin --prune

```
