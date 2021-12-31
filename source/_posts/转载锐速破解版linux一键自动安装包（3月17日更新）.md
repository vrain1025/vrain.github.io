---
title: (转载)锐速破解版linux一键自动安装包（3月17日更新）
tags: []
id: '585'
categories:
  - - 网络收集
date: 2017-03-17 09:45:59
---

破解版锐速 linux 一键自动安装包在本贴持续更新，大家可以加收藏夹，以后有更新都会在这个文章同步。 本破解锐速是是无限带宽版的，破解版锐速的一些代码将逐步开源在 [github 这里](https://github.com/91yun/serverspeeder) 。也欢迎大家订阅我的 Twitter, 实时获得最新信息 .[91yun 的 Twitter](https://twitter.com/91yun_org) 锐速破解版自动安装过程中有什么问题都可以到 [91yun 论坛](http://bbs.91yun.org/) 讨论，我尽量解答。（ 91yun 的官方 TG 群： [https://telegram.me/im91yun](https://telegram.me/im91yun) ）

# 破解版锐速最新更新

\=======2017 年 3 月 17 日更新 =========== ：

1.  之前安装了很多依赖库，基本都精简了，已经不主动安装任何依赖库了。
2.  所有提示改成了英文， putty 应该也能正常显示了
3.  把安装包和支持库列表都放到 github ，并把二进制文件移到了洛杉矶服务器，国内下载应该也会比较快了
4.  配置文件增加了流入加速的开启
5.  配置文件增加了默认带宽到 G 口
6.  手动选内核的安装已经恢复，可以查目前支持的 [完整内核列表](https://www.91yun.org/serverspeeder91yun)

另外：重要的事情说三遍！！！ **锐速不支持 Openvz ！！！锐速不支持 Openvz ！！！锐速不支持 Openvz ！！！**

# 你可能需要：

*   openvz 可以通过 UML 的方式安装 BBR+SSR 了，具体可以看《 [openvz 的 UML+BBR+SSR 一键包（测试）， 64M 小内存运行](https://bbs.91yun.org/discussion/65/openvz%E7%9A%84uml-bbr-ssr%E4%B8%80%E9%94%AE%E5%8C%85-%E6%B5%8B%E8%AF%95-64m%E5%B0%8F%E5%86%85%E5%AD%98%E8%BF%90%E8%A1%8C-3%E6%9C%8816%E6%97%A5%E6%9B%B4%E6%96%B0#latest) 》
*   如果你的内核不对，是 Centos 的话请食用《 [教程： CentOS 更换内核，提供锐速可用的内核下载](https://www.91yun.org/archives/795) 》。 debian 和 ubuntu 我不熟，暂时还没一键包，请自行百度 google 。。
*   如果你嫌麻烦，只是想找个好用的 SS ，嫌麻烦又不想花太多钱，租用我的自用精选线路。。。 [想租 SS 的进](https://www.ss100.pw/)
*   如果你想知道一些服务器是否适合你，请食用 [各种评测报告](https://www.91yun.org/?s=%E8%AF%84%E6%B5%8B) 。我每天都会把我尝试的一些 vps 评测报告发出来，大家可以收藏好本站，及时关注。

 

# 锐速破解版安装方法：

1

wget \-N \--no\-check\-certificate https://github.com/91yun/serverspeeder/raw/master/serverspeeder.sh && bash serverspeeder.sh

如果上面新的安装代码有问题，你依然可以使用以前的旧代码来进行安装：

1

wget \-N \--no\-check\-certificate https://raw.githubusercontent.com/91yun/serverspeeder/master/serverspeeder-all.sh && bash serverspeeder-all.sh

# 锐速破解版卸载方法：

1

chattr \-i /serverspeeder/etc/apx\* && /serverspeeder/bin/serverSpeeder.sh uninstall \-f

 

# 锐速破解版功能：

如果内核完全匹配就会自动下载安装。 如果没有完全匹配的内核，会在界面提示可选内核，可以手动选个最接近的尝试 自动下载授权文件 自动修改配置文件 已 chattr +i /serverspeeder/etc/apx\* 禁止修改配置文件，可以不用加 hosts 了 目前只支持 CentOS ， ubuntu 和 debian 。如果有其他系统支持，可以到 https://www.91yun.org/serverspeeder91yun 手动下载其他系统的安装包 ![QQ图片20160302161200](http://gcsee.com/wp-content/uploads/2017/03/20170317014600116.png)   =======2016 年 8 月 7 日更新 =========== ：

*   新增了以下支持的内核，欢迎大家测试，有问题及时反馈：
    *   CentOS-6.8 ： 2.6.32-642.el7.x86\_64
    *   CentOS-7.2 ： 3.10.0-327.el7.x86\_64
    *   CentOS ： 4.4.0-x86\_64-[linode](https://www.91yun.org/go/linode "linode")63
    *   Ubuntu\_14.04 ： 4.2.0-35-generic
    *   Debian\_8 ： 3.16.0-4-amd64

  =======2016 年 6 月 5 日更新 =========== ：

*   把一直被吐槽的 release\_lsb 的安装代码改了下。。
*   增加了网卡非 eth0 的错误提示。本破解已经确认无法支持网卡名称非 eth0 的网卡。请自行修改《 [CentOS 更换网卡名称](https://www.91yun.org/archives/1217) 》
*   改了下锐速的安装脚本
    *   安装过程中原来有要手动输入加速网卡，上下行带宽等都取消了，采用默认的方式安装。如果有需要修改的朋友请安装完后直接修改锐速的配置文件：
        
        > vi /serverspeeder/etc/config
        
    *   把原来配置文件默认 accppp 的默认改为 0 了。避免没有安装 ppp 服务的机子安装过程中报错。
    *   修复了 centos7 安装的时候可能不会自动随机启动的问题
    *   已知问题： debian 无法随机自动启动，请自行手动把“ /serverspeeder/bin/serverSpeeder.sh start ”加入 rc.local 启动

\=======2016 年 3 月 24 日更新 =========== ：

*   换了种更简单的方式取 mac 地址。如果以前能取到，现在取不到请告知我，谢谢。
*   可以自己填 mac 地址了。使用方法： bash serverspeeder-all.sh mac 地址   就是运行命令后面跟上 mac 地址的参数。比如 :
    
    > bash serverspeeder-all.sh 52:54:00:D3:0F:6C
    

另外：重要的事情说三遍！！！ =======2016 年 3 月 16 日更新 ===========

*   修改了内核匹配机制，在不跨大版本的全部内核里面匹配，提高匹配成功率（比如如果你装的是 Centos6.7 ，但是内核和一个 Centos6.4 一样，就会安装 6.4 的内核）。同样内核的情况下，大部分情况是可以通用的。（如果有问题可以联系我再验证）
*   关于内核不匹配的问题，可以看《 [教程： CentOS 更换内核，提供锐速可用的内核下载](https://www.91yun.org/archives/795) 》
*   添加了自动启动项。（因为发现有些系统重启不会自动启动）
*   PS ：发现有用户如果网卡的名称不是 eth0 的话安装不了，如果有这种情况，请联系我，我需要类似的情况作些测试。谢谢。