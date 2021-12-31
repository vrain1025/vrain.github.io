---
title: VMware 安装苹果系统 禁用CPU
tags: []
id: '930'
categories:
  - - 个人原创
date: 2020-08-06 15:11:33
---

如果你在虚拟机上安装苹果系统时出现：客户机操作系统已禁用 CPU。请关闭或重置虚拟机。

![](https://gcsee.com/wp-content/uploads/2020/08/2020-08-06_150559.jpg)

如果你是 AMD  Ryzen CPU ，而且你的VM 版本是15.1以上，那么解决方法就是 首先，把VM降级到15.1，目前为止，AMD  Ryzen CPU ，没法在15.5 的VM 上安装MACOS。各种办法我都试过了，都不行，国外也有相同的结论。VM版本降后，安装就很简单了。