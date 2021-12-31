---
title: MYSQL 故障导致服务器WEB无法访问
tags: []
id: '537'
categories:
  - - 个人原创
date: 2016-07-01 14:48:32
---

今天上午连接WEB服务器出现问题，同个服务器的页面均无法打开，但是能ping通域名，解析正常，shell到服务器看了一下状态，一切正常，然后重启WEB服务时MYSQL一直在终止，正好服务器有段时间没有重启了，就直接重启服务器了，shell连接工具中断后，很久无法连接到服务器，登陆到服务器的WEB控制台，consle看到服务器还是一直在终止MYSQL服务，直接在控制台强制重启服务器后，shell工具能正常连接到服务器，但是WEB服务还是无法正常显示，查看MYSQL运行状态，发现MYSQL无法启动，手动启动，提示：MySQL is not running, but lock file (/var/lock/subsys/mysql) exists 。然后，刷除/var/lock/subsys/mysql 后再启动，提示The server quit without updating PID file 。然后 用 df -h 命令，一看磁盘居然使用了100%，查看一个网站占用不过500MB，那其它的到底是什么呢，首选怀疑是MYSQL出问题了，然后查看MYSQL所在目录，发现 其var文件下，有9G多的文件，都是mysql-bin.000001、mysql- bin.000002等文件是数据库的操作日志 ![2016-07-01_144454](http://gcsee.com/wp-content/uploads/2016/07/2016-07-01_144454-375x250.png)   删除掉后，然后在MYSQL的配置文件中，把log-bin这一行注释掉，重启mysql服务即可。