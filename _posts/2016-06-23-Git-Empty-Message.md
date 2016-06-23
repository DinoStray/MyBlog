---
layout: post
title: git commit 无注释提交
category: Dev-tools
tags: [git,commit,empty]
---
## git commit 无注释提交
使用git管理非代码类文档， 如笔记，blog等， commit时的message大多略显多余。

```shell
git config --global alias.nccommit 'commit -a --allow-empty-message -m ""'
```

设置别名后， 以后可以直接`git nccommit`无message提交啦
