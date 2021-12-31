---
title: Artisteer制作的主题如何使用WP-Postviews 统计日志浏览次数
tags: []
id: '81'
categories:
  - - 个人原创
date: 2011-04-18 13:28:12
---

采用Artisteer制作的主题和其它手工制作的主题会有很多地方不同，WP-Postviews代码的放置位置也不一样，（对了，忘记说了，本站采用Artisteer制作的主题，嘿嘿，本人比较懒，又不想和别人用一样的主题，就拿Artisteer简单的改了个主题出来）---转入正题，Artisteer制作的主题，找到 \\主题名\\templates\\post\_metadataheader文件，在<?php echo $postheadericons; ?>下插入一行<?php if(function\_exists('the\_views')) { the\_views(); } ?>，OK，完工，，如果你首页没有正常显示统计，那就网上搜一下WP-Postviews的设置教程吧。