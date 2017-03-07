---
layout: post
title: git commit 无注释提交
category: Dev-tools
tags: [git,commit,empty]
---
使用git管理非代码类文档, 如笔记, blog 等, commit 时的 message 有时略显多余。

```shell
git config --global alias.nccommit 'commit -a --allow-empty-message -m ""'
```

设置别名后， 可以直接 `git nccommit` 无注释提交啦
