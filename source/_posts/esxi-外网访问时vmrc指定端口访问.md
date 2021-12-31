---
title: ESXI 外网访问时VMRC指定端口访问
tags: []
id: '919'
categories:
  - - 个人原创
date: 2020-07-22 15:06:00
---

由于国内大部分的公网IP 80端口和443端口都被封了，服务器访问产生很多不便。现有一台企业级服务器，已经安装了ESXI，在内网访问时，VMRC启动是没有任何问题的， 在外网时，由于把443端口映射成666，外网的WEB访问没有什么问题，用https://gcsee.com:666 就可以打开WEB登陆页面。

![](https://gcsee.com/wp-content/uploads/2020/07/1-1024x500.jpg)

但是登陆后，如果想用VMRC操作某台虚拟机，就会出现连接超时的现像。

![](https://gcsee.com/wp-content/uploads/2020/07/04-721-1024x500.jpg)

其实可以用指定端口号和ID的方式来启动远程，直接输入ROOT密码进入。

安装好VMRC在浏览器中输入 vmrc://主机IP:端口号/?moid=虚拟主机ID

例子：vmrc://gcsee.com:666/?moid=1

这次会弹出VMRC的登陆页面，输入root 帐号和密码，即可管理虚拟主机。

![](https://gcsee.com/wp-content/uploads/2020/07/05-721-1024x624.jpg)