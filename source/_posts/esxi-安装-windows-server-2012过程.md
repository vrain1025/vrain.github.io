---
title: ESXI 安装 Windows Server 2012过程
tags: []
id: '439'
categories:
  - - 个人原创
date: 2013-03-15 15:07:00
---

本文说是过程，其实主要记录安装过程中遇到的问题，及解决方法。装系统我相信大家都会的，要不也不会来看这篇文章。

首先，在ESXI 5.1上装 Windows Server 2012 要先装 ESXI的补丁包打上，我就是因为没有打这个补丁包，然后安装了两天也没装进去。不装这个补丁会卡在正在准备设备，或者在那个四块蓝屏，一个圈一直在那转啊转，转几天也还是在那转，开始在网上找一下，有人说在更新驱动，我想着，就放那慢慢更新吧，结果第二天一来，还在那转。今天才找到正确的方法，话说装Windows Server 2012 正常只有20分钟。

先说一下，ESXI找补丁和打补丁的方法吧。

                     去VMWARE官网下载补丁包下载地址如下：

[http://www.vmware.com/patchmgr/download.portal](http://www.vmware.com/patchmgr/download.portal "http://www.vmware.com/patchmgr/download.portal")

选择ESXI 5.1 然后点Search就行了

[![image](http://www.gcsee.com/wp-content/uploads/2013/03/image_thumb.png "image")](http://www.gcsee.com/wp-content/uploads/2013/03/image.png)

  
目前有两种补丁形式  
第一种：每月提供的补丁包，补丁包名如“ESXi500-201209001” ,这种补丁包要按顺序，先装旧的，再装新的。  
第二种：累积的补丁包，补丁包名如“update-from-esxi5.0-5.0\_update01” ，这种补丁包不需要装旧的补丁，直接装就行

  
一、升级前的准备  
1.关闭要升级主机所有虚拟机，如果不关闭虚拟机，将无法进入主机维护模式。  
2.如果宿主机内的虚拟机使用“挂起”模式，也可以进入主机维护模式，但升级后虚拟机可能无法启动，只能重置启动，但无法保证虚拟机可以正常启动  
3.另若主机加入了HA,则要从HA移出或停用HA  
4.宿主机需要开启SSH模式

开启方法：打开vsphere cilent 如图操作即可

[![image](http://www.gcsee.com/wp-content/uploads/2013/03/image_thumb1.png "image")](http://www.gcsee.com/wp-content/uploads/2013/03/image1.png)

  
二、补丁的安装过程  
1.首先将下载的补丁包传到Esxi 的服务器上，建议上传到/vmfs/volumes/datastore1(这里的数字看你自己的)  
2.用ssh登陆到Esxi 的服务器  
3.输入"esxcli software vib install -d="/vmfs/volumes/Local01/update-from-esxi5.0-5.0\_update01.zip"打补丁 （这里的Local01是假设的路径，你在shell里面，cd /vmfs/volumes/datastore1/ 你会发现，你进的文件夹是一长串字符，这里就是要填写那一长串字符,其实datastore1是一下虚拟目录，那一长串长是物理机真实目录）  
4.打完补丁，重启电脑。

  
三、安装Windwos Server 2012  
1.下载安装光盘  
2.升级完后的Esxi安装的时候会有一个Windows Server 2012 的选项，如图

[![image](http://www.gcsee.com/wp-content/uploads/2013/03/image_thumb2.png "image")](http://www.gcsee.com/wp-content/uploads/2013/03/image2.png)  
3.有了这个安装就没有问题了。

本文内容参考了如下文章，对原作者表示谢意：

[http://bbs.51cto.com/thread-971348-1.html](http://bbs.51cto.com/thread-971348-1.html "http://bbs.51cto.com/thread-971348-1.html")

[http://bbs.51cto.com/thread-971348-1.html](http://bbs.51cto.com/thread-971348-1.html "http://bbs.51cto.com/thread-971348-1.html")