---
title: '黑苹果 遇到 IOPlatformExpert.cpp:1590'
tags: []
id: '470'
categories:
  - - 个人原创
date: 2015-05-03 09:29:49
---

[![P50502-101037](http://gcsee.com/wp-content/uploads/2015/05/P50502-101037-300x225.jpg)](http://gcsee.com/wp-content/uploads/2015/05/P50502-101037.jpg)这两天折腾黑苹果电脑重启次数估计已经达到我一年正常使用一年的重启次数了。前天将分区转成 gpt格式之后，重装黑苹果系统就一直“unable to find driver for this platform：\\“ACPI\\.n"@sourcecache/xnu/xnu-1699.24.8/iokit/kernel/ioplatformexpert.cpp:1590 尝试各种办法无果，前几天用mbr安装的时候就没什么问题，所以系统安装盘没有问题，所以只能是引导出了问题，一直修改clover的配置，可是无论怎么改都不行，最后没办法换成变色龙引导，加 -v -f 直接进入系统，心里那个激动啊。然后，再用clover启动，不用修改什么的就能启动了。网上看了 下，大家遇到unable to find driver for this platform：\\“ACPI\\.n"@sourcecache/xnu/xnu-1699.24.8/iokit/kernel/ioplatformexpert.cpp:15＊＊ 这个问题多是用的clover引导，所以，如果你一直卡在这个界面过不去，换成变色龙引导试试吧，说不定会有惊喜哦。