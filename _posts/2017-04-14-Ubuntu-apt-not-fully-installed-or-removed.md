---
layout: post
title: Ubuntu apt 命令安装软件失败后, 再安装其他软件一直提示错误
category: Dev-tools
tags: [Ubuntu,apt]
---

使用 apt install 命令安装软件失败后, 再安装其他软件, 都会提示有 N 个软件

> not fully installed or removed.

然后反复重新安装, 最后提示

>Errors were encountered while processing:
samba4
E: Sub-process /usr/bin/dpkg returned an error code (1)

解决办法:

删除所有未完整安装的软件包

```shell
sudo apt-get --force-yes remove <package-name>
```

把提示安装失败的软件包, 都用 --force-yes remove 命令卸载, 最后

```shell
sudo apt autoremove
```

再次尝试安装其他软件就没有错误提示了.
