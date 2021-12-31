---
title: ubuntu 18.04 初始化的一些坑
tags: []
id: '907'
categories:
  - - 个人原创
date: 2020-04-15 10:03:44
---

准备搞个ubuntu 系统来编译路由器固件，装完之后，发现一大堆坑，我就不明白了，root用户密码随机生成，是个什么鬼，没有ssh服务端又是什么鬼。这种设计是为了安全？

一、设置root 密码

```
打开终端，输入
sudo passwd
然后输入当前用户的密码后"Enter"。
终端会提示我们输入新的密码并确认，此时的密码就是root新密码。
修改成功后，输入命令
su root
输入你刚设置的密码，切换到管理员权限
```

二、安装ssh服务端

sudo apt-get update

sudo apt-get install openssh-server

sudo service ssh start