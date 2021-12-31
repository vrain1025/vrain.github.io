---
title: RouterOS 5.16 虚拟机安装重启
tags: []
id: '397'
categories:
  - - 个人原创
date: 2012-06-09 15:05:11
---

这两天正在做一个RouterOS 5.16的实验，由于没有真实环境，所以用虚拟机进行安装的，安装完成后，发现ROS 无限重启，找了很久才在网上找到了正确的解决方法，这个问题在VirtualBox里就不存在，应该只存在于VMware 8 以上的版本，所以是虚拟机兼容性问题，解决方法也很简单，如果你已经装好ROS了，那可以按下图设置来操作。

1.首先，选择升级虚拟机

[![image](http://www.gcsee.com/wp-content/uploads/2012/06/image_thumb.png "image")](http://www.gcsee.com/wp-content/uploads/2012/06/image.png)

2.下一步

[![image](http://www.gcsee.com/wp-content/uploads/2012/06/image_thumb1.png "image")](http://www.gcsee.com/wp-content/uploads/2012/06/image1.png)

3.这里是重点，一定要选择Workstation 6 这个版本，我试过了，选Workstation6x-7x都不行，必须是6以下的版本

[![image](http://www.gcsee.com/wp-content/uploads/2012/06/image_thumb2.png "image")](http://www.gcsee.com/wp-content/uploads/2012/06/image2.png)

4.这里选择改变这台虚拟机，下一步之后再启动你的ROS看看，是不是能正常启动了。

[![image](http://www.gcsee.com/wp-content/uploads/2012/06/image_thumb3.png "image")](http://www.gcsee.com/wp-content/uploads/2012/06/image3.png)