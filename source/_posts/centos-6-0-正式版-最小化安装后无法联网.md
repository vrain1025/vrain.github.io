---
title: CentOS 6.0 正式版 最小化安装后无法联网
tags: []
id: '200'
categories:
  - - 未分类
date: 2011-08-05 10:18:35
---

最小化安装，默认网卡是不开机启动的，要把网卡设为开机启动。

一、修改IP地址

修改对应网卡的IP地址的配置文件

\[root@centos\]# vi /etc/sysconfig/network-scripts/ifcfg-eth0

修改以下内容

DEVICE=eth0(描述网卡对应的设备别名，例如ifcfg-eth0的文件中它为eth0)

BOOTPROTO=static(设置网卡获得ip地址的方式，可能的选项为static，dhcp或bootp，分别对应静态指定的ip地址，通过dhcp协议获得的ip地址，通过bootp协议获得的ip地址)

BROADcaST=192.168.0.255(对应的子网广播地址)

HWADDR=00:07:E9:05:E8:B4 (对应的网卡物理地址)

IPADDR=12.168.1.2(如果设置网卡获得ip地址的方式为静态指定，此字段就指定了网卡对应的ip地址)

IPV6INIT=no

IPV6\_AUTOCONF=no

NETMASK=255.255.255.0(网卡对应的网络掩码)

NETWORK=192.168.1.0(网卡对应的网络地址)

ONBOOT=yes(系统启动时是否设置此网络接口，设置为yes时，系统启动时激活此设备)

二、修改dns

修改对应网卡的dns的配置文件

\[root@centos\]# vi /etc/resolv.conf

#加入你所在地的DNS

nameserver 202.101.224.69(填你自己的域名服务器）

nameserver 202.101.224.68(填你自己的域名服务器)

三、重启网络

service network restart