---
title: Apache 出现&ldquo;\xef\xbb\xbf&rdquo;
tags: []
id: '163'
categories:
  - - 未分类
date: 2011-07-27 15:21:00
---

今天新增加一个虚拟服务器，下载到windows编辑的，可能第一次打的时候用记事本打开的，然后上传回服务器，就提示错误，在windowns下用UE改还是不行，在网上找到一个可行的方法，现分享给大家。

用vi打开Apache的配置文件，然后输入以下命令就好了。

  
:set nobomb  
:w

出现这个问题主要是windwos下的记事本自动添加UTF-8的头造成的。希望本文对你有用。