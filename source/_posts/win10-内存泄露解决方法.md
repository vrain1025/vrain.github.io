---
title: win10 内存泄露解决方法
tags: []
id: '569'
categories:
  - - 个人原创
date: 2016-10-28 14:01:31
---

由于办公电脑使用华擎B85 Killer 的主板，该主本板载的是KILLER 网卡芯片，近期，电脑运行过程中总是莫名的卡顿，一看任务管理器，内存占用高达97%以上，可是在用户选项卡中实际使用确连内存的20%都达不到，在网上找了很久都没有找到相关问题的解决方案，![03](http://gcsee.com/wp-content/uploads/2016/10/03-375x250.png)![01](http://gcsee.com/wp-content/uploads/2016/10/01-375x250.png) ![02](http://gcsee.com/wp-content/uploads/2016/10/02-375x250.png) 近期，在远景论坛看到一位网友的回答，才知道问题的所在。原来是系统自带的网络数据监控和和Killer网卡的监控程序冲突，导致 非页面缓存无法释放。解决方法：解管理身份运行命令行，输入 sc config ndu start=disabled ，然后重启电脑就可以解决该问题了。sc config ndu start=disabled 这个命令只是禁用系统的网络数据监控功能，不会对系统造成什么影响。 ![04](http://gcsee.com/wp-content/uploads/2016/10/04-375x250.png)