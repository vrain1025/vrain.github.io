---
title: 给BITLOCKER加密的驱动器增加右键菜单项“手动锁定”
tags: []
id: '644'
categories:
  - - 个人原创
date: 2017-10-08 09:35:15
---

![](https://gcsee.com/wp-content/uploads/2017/10/snipaste20171008_093343-300x169.jpg)转至pcbeta http://bbs.pcbeta.com/viewthread-1676077-1-1.html 将如下代码保存成.reg文件，在电脑中导入注册表，WIN 10会出现中文乱码的情况，手动打开注册表，修改 HKEY\_CLASSES\_ROOT\\Drive\\shell\\runas 中的乱码为锁定即可。 ` Windows Registry Editor Version 5.00 [HKEY_CLASSES_ROOT\Drive\shell\runas] @="BitLocker锁定" "AppliesTo"="(System.Volume.BitLockerProtection:=System.Volume.BitLockerProtection#On OR System.Volume.BitLockerProtection:=System.Volume.BitLockerProtection#Encrypting OR System.Volume.BitLockerProtection:=System.Volume.BitLockerProtection#Suspended) AND System.Volume.BitLockerCanChangePassphraseByProxy:=System.StructuredQueryType.Boolean#True" "Icon"="%SystemRoot%\\System32\\manage-bde.exe" [HKEY_CLASSES_ROOT\Drive\shell\runas\command] @="cmd /v:on /k set bdestr=%1 && set bdedrv=!bdestr:~0,2! && manage-bde.exe -lock !bdedrv! -ForceDismount& exit" `