---
title: Autodesk 3ds Max 2012 错误代码110 解决方法
tags: []
id: '347'
categories:
  - - 未分类
date: 2012-01-13 17:03:32
---

我了个去，一个Autodesk 3ds Max 2012 Design装了整整5个小时，唉，其间重装N次，查找N多资料，均不能解决，最后还是在官方论坛找到了解决方法。

[![image](http://www.gcsee.com/wp-content/uploads/2012/01/image_thumb3.png "image")](http://www.gcsee.com/wp-content/uploads/2012/01/image3.png)

出现这个错误，一般是安装不完整造成的，这个在WIN 7下下常，为什么说正常呢，因为，WIN 7 的UAC造成很多用户不知情的情况下对目录权限进行了修改。安装的时候，有些文件它写不进去，也就造成了错误。

先判断你的问题是否和我一样，不一样的话你就不用看下去了，看下去也只是浪费时间 。出现上图的情况一般是安装完后直接提示激活，不论你在安装的时候是填了序列号，还是选择试用，都是必需激活，没有试用30天的画面。然后，当你点激活，继续的时候先是这个110错误，然后就是20错误，然后软件直接关闭。如果，你是这种情况的话，那说明就是文件夹权限问题造成的。

解决方法（以WIN 7 32位版为例）：

首先，进入C:\\ProgramData\\Autodesk\\Adlm\\ASR 将里面所有文件复制

然后，进入C:\\Documents and Settings\\All Users\\Application Data\\Autodesk\\Adlm\\ASR 将刚复制的文件全部粘贴，有重复的直接全部跳过。

如果你没法将文件复制进来，那么，下载本文中的取得管理员权限的注册表文件，在

C:\\Documents and Settings\\All Users\\Application Data\\Autodesk\\Adlm\\ASR  点右键，管理员取得所有权。然后再复制，就能解决问题。

附：win 7 取得管理员权限注册表文件

[http://115.com/file/cl37l3a7#](http://115.com/file/cl37l3a7# "http://115.com/file/cl37l3a7#")

附：Autodesk 3ds Max 2012 Design 注册机及注册方法

注册机：

[http://115.com/file/bhgqel7d#](http://115.com/file/bhgqel7d# "http://115.com/file/bhgqel7d#")

注册机使用方法：

1.安装时根据你装的选择序列号，注意Design版本序列号不同

> 3ds Max 2012 安装时使用下面的序列号：  
> Serial Number: 666-69696969  
> Product Key: 128D1
> 
> 3ds Max design 2012安装时使用下面的序列号：
> 
> Serial Number: 666-69696969  
> Product Key: 495D1
> 
> 注：以上序列号若出现问题，可尝试替换为 359-23187263, 667-98989898, 400-45454545

  

2.安装完成后，在3ds Max激活界面，选择我具有 Autodesk 提供的激活码，把第一次出来的激活界面关闭后再次选择激活（有时候会出现第一次激活无效）

3.当出现激活界面后，根据自己安装3ds Max的位数（32&64）选择运行注册机（Vista或者windows 7以右键管理员权限运行）

4.复制申请号到注册机，先点击mem patth，再点击generate生成注册码（这是必须的，否则无法激活）。

5.点激活，就可以看到激活画面了。OK，还有其它问题，在本文留言，看到后会及时回答。  

在这里提供一下C:\\Documents and Settings\\All Users\\Application Data\\Autodesk\\Adlm\\ASR 的完整打包，给有需要的人。![红玫瑰](http://www.gcsee.com/wp-content/uploads/2012/01/wlEmoticon-redrose.png)

[http://115.com/file/bhgqjp5j#](http://115.com/file/bhgqjp5j# "http://115.com/file/bhgqjp5j#")