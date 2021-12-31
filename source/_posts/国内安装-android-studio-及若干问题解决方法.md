---
title: 国内安装 Android Studio 及若干问题解决方法
tags: []
id: '512'
categories:
  - - 个人原创
date: 2015-10-13 14:35:36
---

为什么要说国内安装呢，这要感谢我们伟大的祖国，把Android的资源都给封了。想要直接下载，就需要FUCK GFW。对于一个初学者来说，要想直接安装Android Studio还真是不容易。

转入正题：

Android Studio 简介：省略，自己百度去吧

Android Studio 下载： 官网：[http://developer.android.com/sdk/index.html](http://developer.android.com/sdk/index.html)

官网进不去的，直接百度Android Studio下载吧。要让Android Studio 能顺利打开。还需要安装：

Java SE Development Kit (JDK)

Android Software Development Kit (SDK)

详细安装请参考文档：

[http://www.codeproject.com/Articles/800701/Setting-Up-Your-Android-Development-Environment](http://www.codeproject.com/Articles/800701/Setting-Up-Your-Android-Development-Environment)

安装完成第一次启动一直停留在fetching Android sdk compoment information界面

[![wpsAF9C.tmp](http://gcsee.com/wp-content/uploads/2015/10/wpsAF9C.tmp_thumb.jpg "wpsAF9C.tmp")](http://gcsee.com/wp-content/uploads/2015/10/wpsAF9C.tmp_.jpg)

解决方法：

　　1）找到安装的Android Studio目录下的bin目录。找到idea.properties文件，用文本编辑器打开。  
　　2）在idea.properties文件末尾添加一行： disable.android.first.run=true ，然后保存文件。  
　　3）关闭Android Studio后重新启动，便可进入界面。

出现Failed to fetch URL [http://dl-ssl.google.com/android/repository/repository.xml](http://dl-ssl.google.com/android/repository/repository.xml), reason: Connection timed out: connect

是连接GOOGLE服务器超时，这个就算在SDK Manager中勾选了强制使用HTTPS链接也还是不行，所以，还是想办法翻墙吧。

### 离线安装Android SDK

### ![](http://www.eoeandroid.com/data/attachment/album/201211/09/224408ftttgmgdsndtrcry.png)

直接举例：现在要下载Google APIs, Android API 23, revision 1

1.  在同意协议的地方复制要安装的插件的SHA1: 04c5cc1a7c88967250ebba9561d81e24104167db
2.  [![image](http://gcsee.com/wp-content/uploads/2015/10/image_thumb.png "image")](http://gcsee.com/wp-content/uploads/2015/10/image.png)
3.  点击Android SDK Manager右下角的按钮，打开Android SDK Manager Log，将其全选复制到记事本
4.  在记事文本中，查找关键字Google APIs, Android API 23, revision 1
5.  在Found Documentation for Android SDK, API 16, revision 3上方找对应XML地址，也就是[http://dl.google.com/android/repository/addon.xml](http://dl.google.com/android/repository/addon.xml "http://dl.google.com/android/repository/addon.xml")
6.  把[http://dl.google.com/android/repository/addon.xml](http://dl.google.com/android/repository/addon.xml "http://dl.google.com/android/repository/addon.xml")复制到浏览器中打开（自测需要翻墙才能打开），或者直接复制到迅雷等下载工具下载（自测无需翻墙也能下载，可以尝试离线下载）
7.  成功打开xml后搜索上方的SHA值 04c5cc1a7c88967250ebba9561d81e24104167db结果发现其名为google\_apis-23\_r01.zip。
8.  [![image](http://gcsee.com/wp-content/uploads/2015/10/image_thumb1.png "image")](http://gcsee.com/wp-content/uploads/2015/10/image1.png)
9.  6、最终下载地址的两种情况（已发现）：
10.  把对应的xml地址，[http://dl.google.com/android/repository/addon.xml](http://dl.google.com/android/repository/addon.xml "http://dl.google.com/android/repository/addon.xml")，的末尾addon.xml去掉，换成google\_apis-23\_r01.zip
11.  最终结果：https://dl-ssl.google.com/android/repository/google\_apis-23\_r01.zip   
12.  上面的各种压缩包下载回来之后，按下面的说明把文件压缩出来：

android开头的文件解压到platforms目录下  
把market\_licensing-r01.zip解压到market\_licensing目录下  
把tools\_r07-windows.zip解压到tools目录下（提示文件已经存在，全部替换就是了。）  
把docs-3.1\_r01-linux.zip解压到docs  
把samples开头的文件解压到samples目录下  
把platform-tools.r05.windows.zip解压到platform-tools目录下