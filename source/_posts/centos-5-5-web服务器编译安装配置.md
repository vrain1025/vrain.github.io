---
title: CentOS 5.5 WEB服务器编译安装配置
tags: []
id: '20'
categories:
  - - 个人原创
date: 2011-01-14 10:44:04
---

CentOS 5.5 WEB服务器编译安装 安装运行库文件 使用 yum 程序安装所需开发包（以下为标准的 RPM 包名称） # yum install gcc gcc-c++ gcc-g77 flex bison autoconf automake bzip2-devel zlib-devel ncurses-devel libjpeg-devel libpng-devel libtiff-devel freetype-devel pam-devel openssl-devel libxml2-devel #这里我们将编译GD所必须的一些小软件比如libpng,libtiff,freetype,libjpeg,等先用RPM的方式一并安装好，避免手动 编译浪费时间，同时也能避免很多错误，这几个小软件的编译很麻烦。这几个小软件编译错误了，GD当然安装不了，php5的编译当然也没戏了。所以我们抓大 放小，对这些小牛鬼蛇神采取快速简洁的方式进行安装。并且对服务器的性能也不能产生什么影响。另外libxml2系统已经默认安装了，所以我们不需要手工编译了，直接安装它的开发包就行了。 安装Apache 1.       卸载系统已经存在的版本： 下面是针对CentOS 5.5 rpm -qa grep httpd（其它版本的有这个命令获取APACHE及关联文件版本） rpm -e gnome-user-share-0.10-6.el5.i386 rpm -e httpd-2.2.3-11.el5\_1.centos.3 2.开始安装 \[root@bogon tmp\]# wget http://labs.renren.com/apache-mirror/httpd/httpd-2.2.17.tar.bz2 \[root@bogon tmp\]# tar jxvf httpd-2.2.17.tar.bz2 \[root@bogon tmp\]# cd httpd-2.2.17 \[root@bogon tmp\]# ./configure --prefix=/usr/local/apache --enable-so \[root@bogon tmp\]# make \[root@bogon tmp\]# make install 安装完成！ \[root@bogon tmp\]#/usr/local/apache/bin/apachectl -k start 开启服务 访问测试 安装MYSQL 5.58 1.由于MYSQL 5.5.8 采用CMAKE编译，所以要先装好CMAKE，才能进行安装MYSQL \[root@bogontmp\]#wget http://mysql.cdpa.nsysu.edu.tw/Downloads/MySQL-5.5/mysql-5.5.8.tar.gz \[root@bogon tmp\]# wget [http://www.cmake.org/files/v2.8/cmake-2.8.3.tar.gz](http://www.cmake.org/files/v2.8/cmake-2.8.3.tar.gz) \[root@bogon tmp\]# tar zxvf cmake cmake-2.8.3.tar.gz \[root@bogon tmp\]#cd cmake-2.8.3 \[root@bogon tmp\]#./configure \[root@bogon tmp\]#make \[root@bogon tmp\]#make install 这里安装的是CMAKE的依赖库 \[root@bogon tmp\]# yum -y install ncurses-devel 下面进行MYSQL安装 \[root@bogon tmp\]# tar zxvf mysql-5.5.8.tar.gz \[root@bogon tmp\]# cd mysql-5.5.8 \[root@bogon tmp\]# cmake . \[root@bogon tmp\]# make \[root@bogon tmp\]# make install mysql 官方网站的安装教程网址： http://dev.mysql.com/doc/refman/5.5/en/installing-source-distribution.html

\[root@bogon tmp\]# cp support-files/my-medium.cnf /etc/my.cnf

\[root@bogon tmp\]# cd /usr/local/mysql

\[root@bogon mysql\]# bin/mysql\_install\_db--user=mysql

\[root@bogon mysql\]# chown -R root  .

\[root@bogon mysql\]# chown -R mysql var

\[root@bogon mysql\]# chgrp -R mysql .

\[root@bogon mysql\]# bin/mysqld\_safe

\--user=mysql & 开启mysql

\[root@bogon mysql\]# ./bin/mysql –u root –p

密码为空

\[root@bogon local\]# cp /usr/local/share/mysql/mysql.server /etc/rc.d/init.d/mysqld

\[root@bogon local\]# chkconfig –add mysqld

//增加mysql自启动

\[root@bogon local\]# mysql –u root –p

mysql> use mysql

Database changed

mysql> update user set password=password("66447300") where user="root";

//设置新密码

安装GD支持库 \[root@bogon tmp\]#yum install aclocal libtool //GD的支持库 \[root@bogon php\]# wget http://www.libgd.org/releases/gd-2.0.35.tar.gz \[root@bogon php\]# ./configure --prefix=/usr/local/libgd --with-png=/usr/local/libpng --with-freetype=/usr/local/freetype  --with-jpeg=/usr/local/libjpeg --with-fontconfig=/usr/local/fontconfig \[root@bogon php\]#make \[root@bogon php\]#make install 安装PHP

1、安装PHP http://cn2.php.net/distributions/php-5.3.5.tar.bz2

\[root@bogon tmp\]# wget [http://cn.php.net/distributions/php-5.3.5.tar.bz2](http://cn.php.net/distributions/php-5.3.5.tar.bz2)

\[root@bogon tmp\]# tar jxvf php-5.3.5.tar.bz2

\[root@bogon tmp\]# cd php-5.3.5

\[root@bogon php-5.3.5\]# ./configure --prefix=/usr/local/php --with-config-file-path=/usr/local/lib --with-apxs2=/usr/local/apache /bin/apxs --with-mysql= /usr/local/mysql --with-zlib --enable-mbstring --enable-xml

\-with-apxs2 与 apache的工具apxs配合，产生模块文件到目录/usr/local/apache/modules/，同时也会自动在apache的配置文件中写入一行"LoadModule php5\_module

modules/libphp5.so"；

\-with-mysql=/usr/local/mysql 与mysql整合，如何没装mysql会出错

\[root@bogon php-5.3.2\]#make

\[root@bogon php-5.3.2\]#make install

\[root@server php-5.3.2\]#cp php.ini-development /usr/local/php/lib/php.ini

\[root@server php-5.3.2\]#vi /usr/local/apache/conf/httpd.conf

加入AddType application/x-httpd-php .php（.php前有一个空格）

\[root@localhost conf\]# cd /usr/local/apache/htdocs/

\[root@localhost htdocs\]# vi test.php

重启apache

\[root@localhost htdocs\]# /usr/local/apache/bin/apachectl -k restart

httpd: Syntax error on line 53 of

/usr/local/apache/conf/httpd.conf: Cannot load

/usr/local/apache/modules/libphp5.so into server:

/usr/local/apache/modules/libphp5.so: cannot restore segment prot after reloc:

Permission denied //重启不成功，是SElinux引起的

下面两种方法

1.\[root@localhost htdocs\]# vi /etc/selinux/config

SELINUX=enforcing 改成SELINUX=disabled重启

2.       \[root@localhost htdocs\]#  chcon -c -v -R -u system\_u -r object\_r -t textrel\_shlib\_t /usr/local/apache/modules/libphp5.so 安装Zend Optimizer 官方的安装说明也行简单： 其实说白了，就是在PHP配置文件里面加一行 zend\_extension=/usr/local/zend/ZendGuardLoader.so 注：/usr/local/zend/ZendGuardLoader.so 这个是你的ZendGuardLoader.so存放路径。 下面是官方的安装说明 Zend Guard Loader installation instructions ------------------------------------------- 1. Extract the Zend Loader package. 2. Locate and extract the ZendGuardLoader.so (Linux) or ZendLoader.dll (Windows) that corresponds to your php version. 3. Add the following line to your php.ini file for loading the ZendGuardLoader: Linux and Mac OS X:      zend\_extension=<full\_path\_to\_ZendGuardLoader.so> Windows non-thread safe: zend\_extension=<full\_path\_to\_ZendLoader.dll> 4. Add an aditional line to your php.ini for enabling ZendGuardLoader ; Enables loading encoded scripts. The default value is On zend\_loader.enable=1 5. Optional: following lines can be added your php.ini file for ZendGuardLoader configuration: ; Disable license checks (for performance reasons) zend\_loader.disable\_licensing=0 ; The Obfuscation level supported by Zend Guard Loader. The levels are detailed in the official Zend Guard Documentation. 0 - no obfuscation is enabled zend\_loader.obfuscation\_level\_support=3 ; Path to where licensed Zend products should look for the product license. For more information on how to create a license file, see the Zend Guard User Guide zend\_loader.license\_path= 6. If you use Zend debugger as well, please make sure to load it after the Zend guard Loader 7. If you use ioncube loader, please make sure to load it before Zend guard Loader 8. Restart your Web server. 服务器组件安全设置 #添加PHP支持 AddType application/x-httpd-php .php .phtml AddType application/x-httpd-php-source .phps #安全配置 ServerSignature Off ServerTokens Prod 未完，待续