---
layout: post
title: 设置Ubuntu 16.04侧边栏位置
category: OS
tags: [Ubuntu][sidebar]
---
## 调整sidebar位置
使用以下命令， 把最后的值改为`Left`或`Bottom`， 目前仅支持这两个位置， 注意大小写

```shell
gsettings set com.canonical.Unity.Launcher launcher-position Left
```
