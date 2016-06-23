---
layout: post
title: 设置Android Studio启动依赖JDK
category: Dev-tools
tags: [AS][JDK]
---
## Android Studio不喜欢OpenJDK

启动AS的时候弹出警告：

> "OpenJDK shows intermittent performance and UI issues. We recommend using the Oracle JRE/JDK."

看来AS对OpenJDK支持不好， 研究了一下AS的启动脚本（bin/studio.sh)， 发现如下代码：

```shell
if [ -n "$STUDIO_JDK" -a -x "$STUDIO_JDK/bin/java" ]; then
  JDK="$STUDIO_JDK"
elif [ -x "$IDE_HOME/jre/jre/bin/java" ] && "$IDE_HOME/jre/jre/bin/java" -version > /dev/null 2>&1 ; then
  JDK="$IDE_HOME/jre"
  ...
```
由此分析只要设置STUDIO_JDK这个系统变量， 就可以指定AS运行的JDK了

## 设置Android Studio启动时调用的JDK环境

下载oracle的官方JDK， 解压到{your_oracle_jdk_home}（我的解压目录：/opt/jdk1.8.0_74 ）

`vi ~/.bashrc`

添加一行

> export STUDIO_JDK={your_oracle_jdk_home}

`source ~/.bashrc`

再次启动AS，不再弹出异常提示。

## 确认AS启动时调用的JDK

在AS中点击工具栏 (Help | Show log in files)

可以弹出AS IDE的日志文件夹， 一般为~/.AndroidStudio2.1/system/log, 查看此日志

修改之前的日志：

> INFO -        #com.intellij.idea.Main - JVM: 25.91-b14 (OpenJDK 64-Bit Server VM)

现在的日志：

> INFO -        #com.intellij.idea.Main - JVM: 25.74-b02 (Java HotSpot(TM) 64-Bit Server VM)

OK， 确定修改成功

> 注意: 此方法修改的是AS 这个IDE的运行JDK， 不是你的java、安卓代码的运行JDK， 请勿混淆
