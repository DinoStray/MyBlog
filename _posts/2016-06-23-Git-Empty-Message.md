---
layout: post
title: git commit 无注释提交
category: Dev-tools
tags: [git][commit][empty]
---
## git commit 无注释提交
使用git管理笔记，blog等， 而不是代码时， 每次提交的message就没有必要了。

```shell
git config --global alias.nccommit 'commit -a --allow-empty-message -m ""'
```

设置别名后， 以后提交可以直接`git nccommit`啦
