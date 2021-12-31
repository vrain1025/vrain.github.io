---
title: CentOS 6.3 安装Zimbra 7.2过程
tags: []
id: '424'
categories:
  - - 个人原创
date: 2012-11-06 15:14:00
---

首先在这里跟大家讲一下，大家下载时一定要下载符合的版本，如果你是用的CentOS装Zimbra也要装对应的RHEL的版本，CentOS 6 以上的系统不推荐安装 32位的RHEL 5 32位版否则会有莫明奇妙的问题。而且，Zimbra的论坛里的人也是这样建议的，就是不要装不符合的版本。（由于Zimbra新版本，只支持64位的RHEL 6，所以，CentOS要装新版的Zimbra，就要用64位版的，而且，以后的Zimbra 可能也不会再出32位版的，所发还是建议大家用64位系统，装64位版的Zimbra）

开始安装过程：

首先安装依赖的软件包，当然你也可以编译安装（这里为了省时间就把MYSQL也直接用yum给装上了）

yum -y install sudo perl libstdc++ gpg sqlite gmp sysstat mysql mysql-server bind-utils

然后下载Zimbra，并解包，由于写这个日志的时候我已经将Zimbra 装好了，所以，有些地址什么的就没有了，大家可以直接百度Zimbra的官网很容易找到下载地址

解包之后如果你直接装会出现下面的错误  
ERROR: Installation can not proceeed.  Please fix your /etc/hosts file  
to contain:

<ip> <FQHN> <HN>

Where <IP> is the ip address of the host,  
<FQHN> is the FULLY QUALIFIED host name, and  
<HN> is the (optional) hostname-only portion  

原来这个zimbra的安装脚本会对hosts每行都校验，多一行不行，少一行不行。

他规定了：

必须有127.0.0.1 localhost.domain localhost这行

必须有固定ip 完整域名 机器名HOSTNAME这行

其他的必须删除（这个并没有在安装教程里面提及过

于是删除了hosts里面的其他内容，顺利的安装。

\[root@RHEL5 etc\]# vi hosts

\# Do not remove the following line, or various programs

\# that require network functionality will fail.

127.0.0.1       localhost.localdomain localhost

192.168.1.16  mail.guchuan.info Mailserver

必须要有RHEL5.6主机名。

\[root@RHEL5 sysconfig\]# cat network

NETWORKING=yes

NETWORKING\_IPV6=no

HOSTNAME=Mailserver

这个修改后执行安装，下面步骤直接引用别人的了。我装的时候没有保存

哦，对了还有下面这个提示

You appear to be installing packages on a platform different

than the platform for which they were built.

This platform is CentOS6\_64

Packages found: RHEL6\_64

This may or may not work.

Installation can not continue without manual override.

You can override this safety check with ./install.sh --platform-override

WARNING: Bypassing this check may result in an install or

upgrade that is NOT usable.

所以你在CentOS上装 Zimbra时要选择强制安装的 ./install.sh --platform-override 就是运行这个，下面是安装过程，转自别处，自行参考，其实只需要按几次Y就行了。

Do you agree with the terms of the software license agreement? \[N\] y

Checking for prerequisites...

     FOUND: NPTL

     FOUND: sudo-1.7.2p1-10

     FOUND: libidn-0.6.5-1.1

     FOUND: gmp-4.1.4-10

     FOUND: /usr/lib/libstdc++.so.6

Checking for suggested prerequisites...

     FOUND: perl-5.8.8

     FOUND: sysstat

     FOUND: sqlite

Prerequisite check complete.

Checking for installable packages

Found zimbra-core

Found zimbra-ldap

Found zimbra-logger

Found zimbra-mta

Found zimbra-snmp

Found zimbra-store

Found zimbra-apache

Found zimbra-spell

Found zimbra-convertd

Found zimbra-memcached

Found zimbra-proxy

Found zimbra-archiving

Found zimbra-cluster

Select the packages to install

Install zimbra-ldap \[Y\] y

Install zimbra-logger \[Y\] y

Install zimbra-mta \[Y\] y

Install zimbra-snmp \[Y\] y

Install zimbra-store \[Y\] y

Install zimbra-apache \[Y\] y

Install zimbra-spell \[Y\] y

Install zimbra-convertd \[Y\] y

Install zimbra-memcached \[N\] y

Install zimbra-proxy \[N\] y

Install zimbra-archiving \[N\] y

Checking required space for zimbra-core

checking space for zimbra-store

Installing:

    zimbra-core

    zimbra-ldap

    zimbra-logger

    zimbra-mta

    zimbra-snmp

    zimbra-store

    zimbra-apache

    zimbra-spell

    zimbra-convertd

    zimbra-memcached

    zimbra-proxy

    zimbra-archiving

The system will be modified.  Continue? \[N\] y

Removing /opt/zimbra

Removing zimbra crontab entry...done.

done.

Cleaning up zimbra init scripts...done.

Cleaning up /etc/ld.so.conf...done.

Cleaning up /etc/prelink.conf...done.

Cleaning up /etc/security/limits.conf...done.

Finished removing Zimbra Collaboration Suite.

Installing packages

Installing packages

    zimbra-core......zimbra-core-7.0.1\_GA\_3105.RHEL5-20110304195331.i386.rpm...done

    zimbra-ldap......zimbra-ldap-7.0.1\_GA\_3105.RHEL5-20110304195331.i386.rpm...done

    zimbra-logger......zimbra-logger-7.0.1\_GA\_3105.RHEL5-20110304195331.i386.rpm...done

    zimbra-mta......zimbra-mta-7.0.1\_GA\_3105.RHEL5-20110304195331.i386.rpm...done

    zimbra-snmp......zimbra-snmp-7.0.1\_GA\_3105.RHEL5-20110304195331.i386.rpm...done

    zimbra-store......zimbra-store-7.0.1\_GA\_3105.RHEL5-20110304195331.i386.rpm...done

    zimbra-apache......zimbra-apache-7.0.1\_GA\_3105.RHEL5-20110304195331.i386.rpm...done

    zimbra-spell......zimbra-spell-7.0.1\_GA\_3105.RHEL5-20110304195331.i386.rpm...done

    zimbra-convertd......zimbra-convertd-7.0.1\_GA\_3105.RHEL5-20110304195331.i386.rpm...done

    zimbra-memcached......zimbra-memcached-7.0.1\_GA\_3105.RHEL5-20110304195331.i386.rpm...done

    zimbra-proxy......zimbra-proxy-7.0.1\_GA\_3105.RHEL5-20110304195331.i386.rpm...done

    zimbra-archiving......zimbra-archiving-7.0.1\_GA\_3105.RHEL5-20110304195331.i386.rpm...done

Operations logged to /tmp/zmsetup.03222011-000215.log

Installing LDAP configuration database...done.

Setting defaults...

DNS ERROR resolving MX for mail.andy.com

It is suggested that the domain name have an MX record configured in DNS

Change domain name? \[Yes\] no

done.

Checking for port conflicts

Main menu

   1) Common Configuration:                                                 

   2) zimbra-ldap:                             Enabled                      

   3) zimbra-store:                            Enabled                      

        +Create Admin User:                    yes                          

        +Admin user to create:                 admin@mail.andy.com          

\*\*\*\*\*\*\* +Admin Password                        UNSET                        

        +Anti-virus quarantine user:           virus-quarantine.vltfq281@mail.andy.com

        +Enable automated spam training:       yes                          

        +Spam training user:                   spam.m94sebkr@mail.andy.com  

        +Non-spam(Ham) training user:          ham.waomqvol@mail.andy.com   

        +SMTP host:                            mail.andy.com                

        +Web server HTTP port:                 80                           

        +Web server HTTPS port:                443                          

        +Web server mode:                      http                         

        +IMAP server port:                     7143                         

        +IMAP server SSL port:                 7993                         

        +POP server port:                      7110                         

        +POP server SSL port:                  7995                         

        +Use spell check server:               yes                          

        +Spell server URL:                     http://mail.andy.com:7780/aspell.php

        +Enable version update checks:         TRUE                         

        +Enable version update notifications:  TRUE                         

        +Version update notification email:    admin@mail.andy.com          

        +Version update source email:          admin@mail.andy.com          

\*\*\*\*\*\*\* +License filename:                     UNSET                        

   4) zimbra-mta:                              Enabled                      

   5) zimbra-snmp:                             Enabled                      

   6) zimbra-logger:                           Enabled                      

   7) zimbra-spell:                            Enabled                      

   8) zimbra-proxy:                            Enabled                      

   9) zimbra-convertd:                         Enabled                      

  10) Default Class of Service Configuration:                               

  11) Enable default backup schedule:          yes                          

   r) Start servers after configuration        yes                          

   s) Save config to file                                                   

   x) Expand menu                                                           

   q) Quit                                   

\--------------------------------------------------------

有\*\*\*的2项内容

\*\*\*\*\*\*\* +Admin Password                        UNSET  

admin@mail.andy.com没有设置口令

\*\*\*\*\*\*\* +License filename:                     UNSET      

导入License

\------------------------------------------------------------

Address unconfigured (\*\*) items  (? - help) 3

Store configuration

   1) Status:                                  Enabled                      

   2) Create Admin User:                       yes                          

   3) Admin user to create:                    admin@mail.andy.com          

\*\* 4) Admin Password                           UNSET                        

   5) Anti-virus quarantine user:              virus-quarantine.vltfq281@mail.andy.com

   6) Enable automated spam training:          yes                          

   7) Spam training user:                      spam.m94sebkr@mail.andy.com  

   8) Non-spam(Ham) training user:             ham.waomqvol@mail.andy.com   

   9) SMTP host:                               mail.andy.com                

  10) Web server HTTP port:                    80                           

  11) Web server HTTPS port:                   443                          

  12) Web server mode:                         http                         

  13) IMAP server port:                        7143                         

  14) IMAP server SSL port:                    7993                         

  15) POP server port:                         7110                         

  16) POP server SSL port:                     7995                         

  17) Use spell check server:                  yes                          

  18) Spell server URL:                        http://mail.andy.com:7780/aspell.php

  19) Enable version update checks:            TRUE                         

  20) Enable version update notifications:     TRUE                         

  21) Version update notification email:       admin@mail.andy.com          

  22) Version update source email:             admin@mail.andy.com          

\*\*23) License filename:                        UNSET                        

Select, or 'r' for previous menu \[r\] 4

Password for admin@mail.andy.com (min 6 characters): \[6FfQR0P8A\] 123456

Store configuration

   1) Status:                                  Enabled                      

   2) Create Admin User:                       yes                          

   3) Admin user to create:                    admin@mail.andy.com          

   4) Admin Password                           set                          

   5) Anti-virus quarantine user:              virus-quarantine.vltfq281@mail.andy.com

   6) Enable automated spam training:          yes                          

   7) Spam training user:                      spam.m94sebkr@mail.andy.com  

   8) Non-spam(Ham) training user:             ham.waomqvol@mail.andy.com   

   9) SMTP host:                               mail.andy.com                

  10) Web server HTTP port:                    80                           

  11) Web server HTTPS port:                   443                          

  12) Web server mode:                         http                         

  13) IMAP server port:                        7143                         

  14) IMAP server SSL port:                    7993                         

  15) POP server port:                         7110                         

  16) POP server SSL port:                     7995                         

  17) Use spell check server:                  yes                          

  18) Spell server URL:                        http://mail.andy.com:7780/aspell.php

  19) Enable version update checks:            TRUE                         

  20) Enable version update notifications:     TRUE                         

  21) Version update notification email:       admin@mail.andy.com          

  22) Version update source email:             admin@mail.andy.com          

\*\*23) License filename:                        UNSET                        

Select, or 'r' for previous menu \[r\] 23

Enter the name of the file that contains the license: /opt/ZCSLicense.xml

Store configuration

   1) Status:                                  Enabled                      

   2) Create Admin User:                       yes                          

   3) Admin user to create:                    admin@mail.andy.com          

   4) Admin Password                           set                          

   5) Anti-virus quarantine user:              virus-quarantine.vltfq281@mail.andy.com

   6) Enable automated spam training:          yes                          

   7) Spam training user:                      spam.m94sebkr@mail.andy.com  

   8) Non-spam(Ham) training user:             ham.waomqvol@mail.andy.com   

   9) SMTP host:                               mail.andy.com                

  10) Web server HTTP port:                    80                           

  11) Web server HTTPS port:                   443                          

  12) Web server mode:                         http                         

  13) IMAP server port:                        7143                         

  14) IMAP server SSL port:                    7993                         

  15) POP server port:                         7110                         

  16) POP server SSL port:                     7995                         

  17) Use spell check server:                  yes                          

  18) Spell server URL:                        http://mail.andy.com:7780/aspell.php

  19) Enable version update checks:            TRUE                         

  20) Enable version update notifications:     TRUE                         

  21) Version update notification email:       admin@mail.andy.com          

  22) Version update source email:             admin@mail.andy.com          

Select, or 'r' for previous menu \[r\] r

Main menu

   1) Common Configuration:                                                 

   2) zimbra-ldap:                             Enabled                      

   3) zimbra-store:                            Enabled                      

   4) zimbra-mta:                              Enabled                      

   5) zimbra-snmp:                             Enabled                      

   6) zimbra-logger:                           Enabled                      

   7) zimbra-spell:                            Enabled                      

   8) zimbra-proxy:                            Enabled                      

   9) zimbra-convertd:                         Enabled                      

  10) Default Class of Service Configuration:                               

  11) Enable default backup schedule:          yes                          

   r) Start servers after configuration        yes                          

   s) Save config to file                                                   

   x) Expand menu                                                           

   q) Quit                                   

\*\*\* CONFIGURATION COMPLETE - press 'a' to apply

Select from menu, or press 'a' to apply config (? - help)

Select from menu, or press 'a' to apply config (? - help) a

Save configuration data to a file? \[Yes\] y

Save config in file: \[/opt/zimbra/config.14607\]

Saving config in /opt/zimbra/config.14607...done.

The system will be modified - continue? \[No\] yes

Operations logged to /tmp/zmsetup.03222011-000215.log

Setting local config values...done.

Setting up CA...done.

Deploying CA to /opt/zimbra/conf/ca ...done.

Creating SSL certificate...done.

Installing mailboxd SSL certificates...done.

Initializing ldap...done.

Setting replication password...done.

Setting Postfix password...done.

Setting amavis password...done.

Setting nginx password...done.

Creating server entry for mail.andy.com...done.

Saving CA in ldap ...done.

Saving SSL Certificate in ldap ...done.

Setting spell check URL...done.

Setting service ports on mail.andy.com...done.

Adding mail.andy.com to zimbraMailHostPool in default COS...done.

Installing webclient skins...

        tree...done.

        sky...done.

        waves...done.

        lavender...done.

        pebble...done.

        sand...done.

        bones...done.

        steel...done.

        smoke...done.

        oasis...done.

        twilight...done.

        carbon...done.

        bare...done.

        lemongrass...done.

        beach...failed.

        hotrod...failed.

        lake...done.

Finished installing webclient skins.

Setting zimbraFeatureTasksEnabled=TRUE...done.

Setting zimbraFeatureBriefcasesEnabled=TRUE...done.

Setting convertd URL...done.

Setting MTA auth host...done.

Setting TimeZone Preference...done.

Initializing mta config...done.

Setting services on mail.andy.com...done.

Creating domain mail.andy.com...done.

Setting default domain name...done.

Setting up default domain admin UI components..done.

Granting group zimbraDomainAdmins@mail.andy.com domain right +domainAdminConsoleRights on mail.andy.com...done.

Granting group zimbraDomainAdmins@mail.andy.com global right +domainAdminZimletRights...done.

Setting up global distribution list admin UI components..done.

Granting group zimbraDLAdmins@mail.andy.com global right +adminConsoleDLRights...done.

Granting group zimbraDLAdmins@mail.andy.com global right +listAccount...done.

Creating domain mail.andy.com...already exists.

Creating admin account admin@mail.andy.com...done.

Creating root alias...done.

Creating postmaster alias...done.

Creating user spam.m94sebkr@mail.andy.com...done.

Creating user ham.waomqvol@mail.andy.com...done.

Creating user virus-quarantine.vltfq281@mail.andy.com...done.

Setting spam training and Anti-virus quarantine accounts...done.

Initializing store sql database...done.

Setting zimbraSmtpHostname for mail.andy.com...done.

Configuring SNMP...done.

Checking for default IM conference room...not present.

Initializing default IM conference room...done.

Setting up syslog.conf...done.

Setting default backup schedule...Done

Looking for valid license to install...license installed.

Starting servers...done.

Installing common zimlets...

        com\_zimbra\_adminversioncheck...done.

        com\_zimbra\_webex...done.

        com\_zimbra\_url...done.

        com\_zimbra\_dnd...done.

        com\_zimbra\_linkedin...done.

        com\_zimbra\_cert\_manager...done.

        com\_zimbra\_date...done.

        com\_zimbra\_attachmail...done.

        com\_zimbra\_srchhighlighter...done.

        com\_zimbra\_email...done.

        com\_zimbra\_bulkprovision...done.

        com\_zimbra\_social...done.

        com\_zimbra\_attachcontacts...done.

        com\_zimbra\_phone...done.

Finished installing common zimlets.

Installing network zimlets...

        com\_zimbra\_convertd...done.

        com\_zimbra\_hsm...done.

        com\_zimbra\_backuprestore...done.

        com\_zimbra\_license...done.

        com\_zimbra\_xmbxsearch...done.

        com\_zimbra\_mobilesync...done.

        com\_zimbra\_delegatedadmin...done.

Finished installing network zimlets.

Restarting mailboxd...done.

Setting up zimbra crontab...done.

Moving /tmp/zmsetup.03222011-000215.log to /opt/zimbra/log

Configuration complete - press return to exit

安装完成后用

du -sh zimbra/ 查看空间占用

netstat –ltnp 查看运行端口情况

然后，你就可以通过IP地址或域名登陆WEB管理界面了

[![2012-11-06_151234](http://www.gcsee.com/wp-content/uploads/2012/11/2012-11-06_151234_thumb.jpg "2012-11-06_151234")](http://www.gcsee.com/wp-content/uploads/2012/11/2012-11-06_151234.jpg)

登陆后界面

[![2012-11-06_151352](http://www.gcsee.com/wp-content/uploads/2012/11/2012-11-06_151352_thumb.jpg "2012-11-06_151352")](http://www.gcsee.com/wp-content/uploads/2012/11/2012-11-06_151352.jpg)