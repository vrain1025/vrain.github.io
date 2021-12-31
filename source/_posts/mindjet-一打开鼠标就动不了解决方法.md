---
title: Mindjet 一打开鼠标就动不了解决方法
tags: []
id: '428'
categories:
  - - 个人原创
date: 2012-12-05 17:19:00
---

在网上查找了一下相关资料，这个主要是Mindjet不支持64位系统造成的，其实就和Windows tablet pc input 这个服务相冲突造成的，临时的解决方法是，win+r （别告诉我你不知道哪个是WINDOWS键，四块屏那个键），然后输入 CMD，然后输入 net stop "tablet pc input service" 再输入 net start "tablet pc input service" 鼠标就恢复了。这个方法十分不方便，下面来告诉大家一个一劳永逸的方法

1.打开 c:/windows/system32文件夹

2.找到wisptis.exe这个程序，然后属性--高级--将所有者改成你现在用的用户

[![image](http://www.gcsee.com/wp-content/uploads/2012/12/image_thumb.png "image")](http://www.gcsee.com/wp-content/uploads/2012/12/image.png)

3.直接删除，（我是用unlocker删除的，不知道能不能直接删除）

再次打开Mindjet ，就不会出现鼠标假死了，不过貌似Mindjet 打开的有点慢，我电脑问题？