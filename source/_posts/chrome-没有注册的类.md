---
title: chrome 没有注册的类
tags: []
id: '467'
categories:
  - - 个人原创
date: 2015-04-06 07:54:31
---

近期重装win 8.1 后，系统总是出现莫名的问题，按理说装的MSDN版的，不应该啊，首先是系统运行软件需要管理员权限的软件会提示错误，这个最后发现是和StartIsBack冲突了，卸载后解决，现在Chrome又出现没有注册的类，查了一下，需要删除注册表中类似\[HKEY\_CLASSES\_ROOT\\Chrome.XLXQHAVXIJLDRSLG5HCERTD6TA\\.exe\] 的键值。然后在 控制面板\\程序\\默认程序\\设置默认程序 中 选择Chrome 并将此程序设为默认值。