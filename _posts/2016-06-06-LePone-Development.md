---
layout: post
title: 使用乐视2 x2手机调试开发注意事项
category: 乐视
tags: [乐视,手机,日志]
---

下面介绍怎样开启输出全部日志和查询硬件信息

## 开启全部日志
乐视手机默认只输出Info以下级别日志, Verbose和Debug均不输出

在拨号界面输入`*#*#76937#*#*`

Tips:
1. 注意数字下方的英文字母, 这串数字其实对应单词"power"
* 注意截图没有输入最后一位符号

![*#*#76937#*#*](http://7xoj7k.com1.z0.glb.clouddn.com/md_%E4%B9%90%E8%A7%86%E6%89%8B%E6%9C%BA%E8%AE%BE%E7%BD%AE%E6%97%A5%E5%BF%97%E8%BE%93%E5%87%BA_%E6%8B%A8%E5%8F%B7%E7%95%8C%E9%9D%A2_01.png)

如下图选中"Enable All Logs"

![Enable All Logs](http://7xoj7k.com1.z0.glb.clouddn.com/16-6-3/24273146.jpg)

## 查询硬件信息
如需查询IMEI等信息, 可以在拨号界面输入`*#5388#*`

![*#5388#*](http://7xoj7k.com1.z0.glb.clouddn.com/md_%E4%B9%90%E8%A7%86%E6%89%8B%E6%9C%BA%E6%9F%A5%E8%AF%A2IMEI_%E6%8B%A8%E5%8F%B7%E7%95%8C%E9%9D%A2_01.png)

点击"固件信息", 即可查询IMEI号等

![固件信息](http://7xoj7k.com1.z0.glb.clouddn.com/md_%E4%B9%90%E8%A7%86%E6%89%8B%E6%9C%BA%E6%9F%A5%E8%AF%A2%E5%9B%BA%E4%BB%B6%E4%BF%A1%E6%81%AF_01.png)

因为是双卡手机, 会有两个IMEI号码

![IMEI信息](http://7xoj7k.com1.z0.glb.clouddn.com/md_%E4%B9%90%E8%A7%86%E6%89%8B%E6%9C%BA%E6%9F%A5%E8%AF%A2%E5%9B%BA%E4%BB%B6%E4%BF%A1%E6%81%AF_02.png)
