---
title: vultr Cent  OS 初始化过程
tags: []
id: '588'
categories:
  - - 个人原创
date: 2017-03-21 15:46:55
---

SSR一键安装脚本 wget -N --no-check-certificate https://raw.githubusercontent.com/91yun/shadowsocks\_install/master/shadowsocksR.sh && bash shadowsocksR.sh 卸载方法： bash ./shadowsocksR.sh uninstall   端口：10001 密码：66447300 升级方法： cd /usr/local/shadowsocks/shadowsocks git pull使用命令： 启动： /etc/init.d/shadowsocks start 停止： /etc/init.d/shadowsocks stop 重启： /etc/init.d/shadowsocks restart 状态： /etc/init.d/shadowsocks status 配置文件路径： /etc/shadowsocks.json 日志文件路径： /var/log/shadowsocks.log 安装路径： /usr/local/shadowsocks/shadowsoks 多用户配置 如果要多个用户一起使用的话，请写入以下配置（ vi /etc/shadowsocks.json ）： 多用户的核心是这个配置，把这个配置替代掉 /etc/shadowsocks.json 的相关密码的配置就行了： “port\_password”:{ “80”:”password1″, “443”:”password2″ }, 完整的多用户配置：

{
    "server":"0.0.0.0",
    "server\_ipv6": "\[::\]",
    "local\_address":"127.0.0.1",
    "local\_port":1080,
    "port\_password":{
        "80":"password1",
        "443":"password2"
    },
    "timeout":300,
    "method":"aes-256-cfb",
    "protocol": "auth\_sha1\_compatible",
    "protocol\_param": "",
    "obfs": "http\_simple\_compatible",
    "obfs\_param": "",
    "redirect": "",
    "dns\_ipv6": false,
    "fast\_open": false,
    "workers": 1
}

如果你想修改配置文件，请参考： https://github.com/breakwa11/shadowsocks-rss/wiki/Server-Setup

* * *

锐速破解版安装方法： wget -N --no-check-certificate https://github.com/91yun/serverspeeder/raw/master/serverspeeder.sh && bash serverspeeder.sh 锐速破解版卸载方法： chattr -i /serverspeeder/etc/apx\* && /serverspeeder/bin/serverSpeeder.sh uninstall -f

* * *