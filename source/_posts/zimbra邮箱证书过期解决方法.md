---
title: zimbra邮箱证书过期解决方法
tags: []
id: '443'
categories:
  - - 网络收集
date: 2013-08-22 16:15:21
---

最近闲来无事，进了一下去年装的zimbra，网页端无法打开，进入服务器看一下连接状态，服务器本身能连上外网，然后在网上找了一下查看zimbra运行状态的方法。进入/opt/zimbra/bin/ 目录 运行zmcontrol status 命令，查看运行状态。

\[zimbra@zcs ~\]$ zmcontrol status   
Unable to determine enabled services from ldap.   
Unable to determine enabled services. Cache is out of date or doesn't exist.

在出现上述的错误时，有4种可能的原因：

1.  ZCS证书的问题
2.  Zimbra文件的权限问题
3.  LDAP数据的问题
4.  DNS问题

这篇文章主要讲解的是证书过期的问题，一般情况，zimbra邮箱服务器搭建使用一年左右的，出现这样的问题，那么首先要考虑的就是证书过期的问题了。

新安装zimbra的时候自己签发的证书有效期是365天，也就是1年。为了避免下次的麻烦，我们可以重新签发一个证书，而且有效期可以自己设定，下面的例子有效期是10年。命令如下:

/opt/zimbra/bin/zmcertmgr createca -new

/opt/zimbra/bin/zmcertmgr deployca

/opt/zimbra/bin/zmcertmgr createcrt -new -days 3650  这后面的数字就是证书的使用年限，以天为单位

/opt/zimbra/bin/zmcertmgr deploycrt self

/opt/zimbra/bin/zmcertmgr viewdeployedcrt

敲完以上的命令后，重启zimbra邮箱服务器，使用 zmcontrol restart命令查看服务是否全部开启，再在客户端上重新收发邮件，如果上面的代码输入正确，邮箱就能正常使用了。