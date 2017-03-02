---
layout: post
title: MinGW CygWin MSYS 比较
category: 工具
tags: [POSIX API,Windows 编程]
---

要比较 MinGW 和 Cygwin, 需要先理解 POSIX.

## POSIX

POSIX( Portable Operating System Interface )是个标准, 定义了操作系统应该为应用程序提供的接口: 系统调用函数. 如果所有操作系统都支持此标准, 那同一套源代码可以在所有系统中编译后运行.

对此标准, windows 敷衍到令人发指, Unix 系统家族却不分你我, 彼此共生.

Linux 与 Unix 这么像的一个原因, 就是他们都遵循 POSIX 标准.

## CygWin

> 在 windows 系统中提供 POSIX 支持

CygWin 通过调用 windows API 实现了大部分 POSIX API, 封装在 cygwin1.dll 中. 进而实现了以下目的:

1. 使调用了 Linux API 的源代码, 通过 Cygwin 重新编译后, 可以运行在 windows
2. 可以在 windows 中开发 Linux 应用

## MinGW

> 仅使用自由软件编译出纯粹的 win32 程序.

**自由软件**

通过移植 GNU 的一系列免费开源软件, 如 GCC 编译套件, 代替微软的收费软件, 如 VS.
利用这些软件来进行 windows 应用的开发.

**纯粹的**

MinGW 明确表示, 永远不会考虑移植 POSIX API, 仅能通过 MinGW 调用 Microsoft C Runtime 和 Windows 系统 API, 所以编译后的应用是纯粹的 win32 应用. 这也是其与 Cygwin 最大的不同.

## MSYS

> 简化版 Cygwin, MinGW 的小伙伴

MSYS 和 MSYS2 均 fork 自 Cygwin, 是 Cygwin 的简化版, 为 MinGW 提供一系列迁移自 Linux 的命令行工具.

## 总结

Cygwin 和 MinGW 虽然产生的目的不同, 但是我中有你, 你中有我的.

MSYS 服务于 MinGW 却 fork 自 Cygwin, 而 Cygwin 中也包含 MinGW 迁移后的 GCC 套件, 用于开发纯粹的 win32 程序.

个人观点:
> 两款软件互利互补, 不存在谁比谁更优秀.  
> Cygwin 显然格局更大, 可以完整包含 MinGW.  
> 目前我所在的项目组就在 Cygwin 中搭建了一套支持 repo 的 android 开发环境, 使用起来非常 high  
> 开发者应该首选 Cygwin.
