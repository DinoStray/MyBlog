---
layout: post
title: Letv android-4.x 编译环境搭建
category: Dev-tools
tags: [Ubuntu,apt]
---

针对公司 Letv android-4.x 系统编译总结, 对 AOSP 版本的 android v4.x 系统应该也有借鉴.

在 Ubuntu Kylin 16 搭建好 AOSP 的 android-2.3.1_r1 编译环境后, 就开始继续搞公司的安卓源码, 本以为 v2.3 这么老的源码都编译好了, 公司的安卓 v4.x 源码应该很顺利了, 结果还是遇到很多问题.

## 版本信息：
OS: Kylin ubuntu 16.04， 基本等同 ubuntu 16.04， 个人偏爱所以选了 Kylin

aosp: Letv android-4

### 其他编译工具版本：
java: oracle jdk 6.0

make: 3.81

gcc: 4.4

perl: 5.18.2

## java 版本

update-alternatives 在安卓 4 构建环境里不好使了, 尽管我切换了 java 版本到 1.6, 在执行了 lunch 命令后, 还是会被切换回 1.8 版本, 所以写了一个专门的 java 执行环境脚本:

```shell
export PATH=/usr/lib/jvm/java-6-oracle/jre/bin:/usr/lib/jvm/java-6-oracle/bin:$PATH
```

保存为 my_env.sh

```shell
chmod 777 my_env.sh
source my_env.sh
```

每次执行完 lunch 后再执行脚本, 这样编译时的 java, javac, javadoc 就都被强制为 1.6 版本了.

这里再提醒下, PATH 中赋值的路径, 结尾处不要添加 / 符号.

如: /usr/lib/jvm/java-6-oracle/jre/bin/ 是错误的

必须 /usr/lib/jvm/java-6-oracle/jre/bin

我没搞懂这两个的区别, 但是加了 / 符号, 会导致源码编译失败, 爆出类似下面的错误:

```shell
external/doclava/src/com/google/doclava/Doclava.java:1286: cannot find symbol
symbol  : class ClassDoc
location: class com.google.doclava.Doclava
      ClassDoc classDoc = (ClassDoc) doc;
      ^
external/doclava/src/com/google/doclava/Doclava.java:1286: cannot find symbol
symbol  : class ClassDoc
location: class com.google.doclava.Doclava
      ClassDoc classDoc = (ClassDoc) doc;
                           ^
external/doclava/src/com/google/doclava/Doclava.java:1295: cannot find symbol
symbol  : class ClassDoc
location: class com.google.doclava.Doclava
      ClassDoc current = classDoc;
      ^
external/doclava/src/com/google/doclava/Doclava.java:1326: cannot find symbol
symbol  : class Doc
location: class com.google.doclava.Doclava
        if ((entry instanceof Doc) && isHidden((Doc) entry)) {
                              ^
external/doclava/src/com/google/doclava/Doclava.java:1326: cannot find symbol
symbol  : class Doc
location: class com.google.doclava.Doclava
        if ((entry instanceof Doc) && isHidden((Doc) entry)) {
                                                ^
external/doclava/src/com/google/doclava/Doclava.java:1362: cannot find symbol
symbol  : class Type
location: class com.google.doclava.Doclava.HideHandler
      if (proxy instanceof Type && methodName.equals("toString")) {
                           ^
Note: external/doclava/src/com/google/doclava/Stubs.java uses unchecked or unsafe operations.
Note: Recompile with -Xlint:unchecked for details.
136 errors
make: *** [out/host/common/obj/JAVA_LIBRARIES/doclava_intermediates/javalib.jar] Error 41
```

## perl版本

Ubuntu 16 中的 Perl 已经是 5.22.1 了, 但编译 安卓 4 需要 5.18.2, 否则编译会报错:

> Can't use 'defined(@array)' (Maybe you should just omit the defined()?) at kernel/timeconst.pl line 373.
make[2]: *** [kernel/timeconst.h] Error 255
make[1]: *** [kernel] Error 2

```shell
wget http://www.cpan.org/src/5.0/perl-5.18.2.tar.gz

解压后进入目录, 配置 perl 的安装目录

./Configure -des -Dprefix=/home/!!你的用户名!!/soft/tools-perl-5.18.2 -Dusethreads -Uversiononly -Dcc=gcc

make
make test
make install
```

安装要等好久, 成功后用 update-alternatives 配置 perl 版本

```shell
配置前需要注意, 虽然环境变量里的 perl 版本变了, 可有的 perl 脚本, 在第一行就指定了运行脚本的命令, 如

#! /usr/bin/perl

没办法, 只好重命名 /usr/bin/perl

mv /usr/bin/perl /usr/bin/perl_5_22

sudo update-alternatives --install ~/bin/perl perl ~/soft/tools-perl-5.18.2/bin/perl 5182
sudo update-alternatives --install ~/bin/perl perl /usr/bin/perl_5_22 5221
sudo update-alternatives --config perl

最后通过软链接链过去

ln ~/bin/perl /usr/bin/perl


```

选择 5.18.2 版本的 perl

然后注意这个异常:

> Can't locate Switch.pm in @INC (you may need to install the Switch module) (@INC contains: /home/vvqboy/soft/tools-perl-5.18.2/lib/site_perl/5.18.2/x86_64-linux-thread-multi /home/vvqboy/soft/tools-perl-5.18.2/lib/site_perl/5.18.2 /home/vvqboy/soft/tools-perl-5.18.2/lib/5.18.2/x86_64-linux-thread-multi /home/vvqboy/soft/tools-perl-5.18.2/lib/5.18.2 .) at external/webkit/Source/WebCore/make-hash-tools.pl line 23.

如果只安装了一个版本的 perl, 用
```shell
sudo apt-get install libswitch-perl
```
可以解决问题.

但多版本的 perl, 就不能依赖 apt 安装 Swtich 了, 则需要切换到指定版本后, 需要用 cpan 命令安装 Swtich

在终端依次输入以下命令:
```shell
cpan
install Switch
exit
```
