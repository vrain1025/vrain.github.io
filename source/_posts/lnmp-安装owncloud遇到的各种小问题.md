---
title: lnmp 安装ownCloud遇到的各种小问题
tags: []
id: '618'
categories:
  - - 个人原创
date: 2017-04-15 14:03:38
---

*   PHP模块'文件信息'丢失. 我们强烈建议启用此模块以便mime类型检测取得最佳结果.

解决方法：安装PHP的fileinfo 扩展 安装方法： 跳转到PHP源文件夹中的扩展文件目录：cd /lnmp\*\*/src/php-5.\*.\*/ext/fileinfo/ PHP 安装目录 /usr/local/php/bin/phpize 返回: Configuring for: PHP Api Version: 20100412 Zend Module Api No: 20100525 Zend Extension Api No: 220100525

```
./configure --with-php-config=/usr/local/php/bin/php-config
make && make install
```

返回如下信息: Build complete. Don't forget to run 'make test'.

```
Installing shared extensions:     /usr/local/php/lib/php/extensions/no-debug-non-zts-20100525/
```

表示OK了! 最后在/usr/local/php/etc/php.ini 添加扩展:

```
extension=fileinfo.so
```

*   PHP 似乎没有设置好查询的系统环境变量。 用 getenv(\\"PATH\\") 测试只返回一个空值。

在php-fpm.conf 中加上 env\[PATH\] = /usr/local/bin:/usr/bin:/bin:/usr/local/php/bin重启一下php-fpm就可以了

*   /dev/urandom 无法被 PHP 读取，出于安全原因，这是强烈不推荐的。请查看文档解详情。

LNMP 1.2及更高版本防跨目录功能使用.user.ini，该文件在网站根目录下，可以修改open\_basedir的值来设置限制目录的访问。 .user.ini文件无法直接修改，可以使用[winscp文件管理](https://www.vpser.net/manage/winscp.html)、[vim编辑器](http://www.vpser.net/manage/vi.html)或[nano编辑器](http://www.vpser.net/manage/nano.html)进行修改。 如要修或删除需要先执行：chattr -i /网站目录/.user.ini 删除的话rm -f /网站目录/.user.ini 就可以。 修改完成后再执行：chattr +i /网站目录/.user.ini