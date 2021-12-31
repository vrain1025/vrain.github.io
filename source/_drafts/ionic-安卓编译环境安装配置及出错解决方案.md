---
title: ionic 安卓编译环境安装配置及出错解决方案
tags: []
id: '594'
categories:
  - - 个人原创
---

1.安装配置JAVA SDK 2.安装安卓 SDK 3.设置好环境变量 4.安装好ionic $ npm install -g ionic cordova

* * *

Download tools\_r25.2.3-windows.zip from Android Downloads. Extracted zip on desktop Replaced C:\\Users\\username\\AppData\\Local\\Android\\sdk\\tools with extracted sub-folder tools/ In project folder:

* * *

$ cordova platforms remove android $ cordova platforms add android 5.在要打包的程序目录下运行 cordova prepare android 6.运行 ionic build android --prod --release