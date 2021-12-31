---
title: win8.1 传统引导模式 转 EFI 引导模式
tags: []
id: '472'
categories:
  - - 个人原创
date: 2015-05-01 11:52:37
---

这两天又在研究黑苹果 ，与以前不同这次不在虚拟机中玩，也不拿笔记本玩了，用我的办公台式机来折腾。唉，一句话，生命不息，折腾不止。就是因为要装黑苹果，所以引导问题就显得很重要了，用传统BIOS引导的话，一是太麻烦了，二是启动慢，所以就有了想用EFI引导的想法，可是现在的系统是MBR分区+传统BIOS引导，我不想重装了，必竟过不多久就要升级windows 10了，所以还是留那时再装吧。所以在研究无损的方法，在10分钟前刚成功，分享下成功经验。 成功后的引导画面我就不上了，直接上系统信息 [![1](http://gcsee.com/wp-content/uploads/2015/05/1-300x170.jpg)](http://gcsee.com/wp-content/uploads/2015/05/1.jpg) 前提条件说明： 1.主板支持EFI引导 2.硬盘分区必须转成GPT 3.64位win7以上系统 4.自己有个能引导的win8PE U盘，大部分操作都是PE下完成，其实操作很简单。 如果不满足以上三个条件，就不要试了。会启动不了的。 下面开始实施过程

1.  U盘启动进入win8PE，运行PE中的DiskGenius Pro ，如果没有，下载网盘中的那个放到U盘就可以了。链接：http://pan.baidu.com/s/1gdvR91T 密码：yq4x
2.  先中磁盘右键，调整分区大小，前面留出300MB即可。(如图2)[![2](http://gcsee.com/wp-content/uploads/2015/05/2-300x237.jpg)](http://gcsee.com/wp-content/uploads/2015/05/2.jpg)[](http://gcsee.com/wp-content/uploads/2015/05/2.jpg)
3.  对前面那空闲的300MB点键，建立分区，分区类型选EFI system partition 简称ESP （如图3）[![3](http://gcsee.com/wp-content/uploads/2015/05/3-300x223.jpg)](http://gcsee.com/wp-content/uploads/2015/05/3.jpg)
4.  格式化分区为 FAT32 并指定盘符为X
5.  然后运行PE中的命令提示符工具 输入 bootbcd c:\\windwos /s x: /f all /l zh-cn  （解释一下bootbcd的作用，这是一个命令行工具，它能够重建和备份系统引导文件 到指定位置就是我们新建的盘符为X的ESP分区）
6.  大功告成了，重启，然后选EFI引导 就可以看到画面了。