---
title: 解决Navicat Premium连接SQL Server报错
tags: []
id: '956'
categories:
  - - 个人原创
date: 2021-11-03 09:15:39
---

新装的Navicat Premium 15 连接SQL SERVER 时会报\[navicat premium\] \[IM002\] \[Microsoft\]\[ODBC 驱动程序管理器\] 未发现数据源名称并且未指定默认驱动程序，这个错误，确认数据库没问题后，查询后发现，需要安装一下Navicat根目录下的msodbcsql\_64.msi，不同版本可能名字不一样，可以在根目录下找一下。安装后即可解决报错问题。