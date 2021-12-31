---
title: openwrt 命令行修改主题
tags: []
id: '940'
categories:
  - - 个人原创
date: 2021-07-29 10:18:34
---

由于自己编译时修改了openwrt的默认主题，刷好的openwrt打开首页空白，怀疑编译的主题有问题，又不想再刷一次机，然后用ssh进路由的页面，可以正常连接，修改默认主题还是很简单，修改一下

/etc/config/luci 文件中的主题名字就行了。

![](https://gcsee.com/wp-content/uploads/2020/11/微信图片_20201127161919.png)