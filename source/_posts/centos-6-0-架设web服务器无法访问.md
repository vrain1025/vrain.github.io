---
title: CentOS 6.0 架设WEB服务器无法访问
tags: []
id: '201'
categories:
  - - 网络收集
date: 2011-08-05 10:26:26
---

首先，用netstat –lntp 看看你的服务器启动了不，如果启动了不能访问那就该看防火墙了，由于CentOS6.0默认安装防火墙而且不开放WEB服务器需要的端口，所以，如果你的WEB服务器不能访问，就要把以下规则加入防火墙。 以下内容收集自网络：

* * *

#/sbin/iptables -I INPUT -p tcp --dport 80 -j ACCEPT  
#/sbin/iptables -I INPUT -p tcp --dport 22 -j ACCEPT  
#/sbin/iptables -I INPUT -p tcp --dport 3306 -j ACCEPT  
然后保存：  
#/etc/rc.d/init.d/iptables save

查看打开的端口：  
\# /etc/init.d/iptables status

* * *

  
补充说明：  
#关闭防火墙  
/etc/init.d/iptables stop  
service iptables stop # 停止服务  
#查看防火墙信息  
/etc/init.d/iptables status  
#开放端口:8080  
/sbin/iptables -I INPUT -p tcp --dport 8080 -j ACCEPT  
#重启防火墙以便改动生效:(或者直接重启系统)  
/etc/init.d/iptables restart  
#将更改进行保存  
/etc/rc.d/init.d/iptables save  
另外直接在/etc/sysconfig/iptables中增加一行：  
\-A RH-Firewall-1-INPUT -m state –state NEW -m tcp -p tcp –dport 8080 -j ACCEPT

#永久关闭防火墙  
chkconfig –level 35 iptables off #此方法源自网络，未实验，安全考虑拒绝使用此方法