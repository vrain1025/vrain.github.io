---
title: Cloudflare API acme 生成 ssl 证书 遇到的问题
tags: []
id: '954'
categories:
  - - 个人原创
date: 2021-07-29 10:51:24
---

1\. 首先根据官方安装说明，安装最新版的ame

`curl https://get.acme.sh sh`

然后按官方指引，申请证书,本文以cloudflare 为例，使用cloudflare API申请，API获取 在Cloudflare 域名首页，右下角，有个获取获取您的 API 令牌，然后获取Global API Key。

`root@instance-1:/home/vrain# export CF_Key="xxxxxxx"  
root@instance-1:/home/vrain# export CF_Email="xx@xx.com"`

`root@instance-1:/home/xx# ~/.acme.sh/acme.sh --issue --dns dns_cf -d xx.cf -d *.xx.cf`

然后，你会看到

\[Thu Jul 29 00:49:44 UTC 2021\] Create account key ok.  
\[Thu Jul 29 00:49:44 UTC 2021\] No EAB credentials found for ZeroSSL, let's get one  
\[Thu Jul 29 00:49:44 UTC 2021\] acme.sh is using ZeroSSL as default CA now.  
\[Thu Jul 29 00:49:44 UTC 2021\] Please update your account with an email address first.  
\[Thu Jul 29 00:49:44 UTC 2021\] acme.sh --register-account -m my@example.com  
\[Thu Jul 29 00:49:44 UTC 2021\] See: https://github.com/acmesh-official/acme.sh/wiki/ZeroSSL.com-CA  
\[Thu Jul 29 00:49:44 UTC 2021\] Please add '--debug' or '--log' to check more details.  
\[Thu Jul 29 00:49:44 UTC 2021\] See: https://github.com/acmesh-official/acme.sh/wiki/How-to-debug-acme.sh

这个报错，我加了--log 后也没看明白，怎么回事，最后查到原因，是因为account文件中没有添加e-mail地址。在/root/.acme.sh/account.conf 加入 ACCOUNT\_EMIAL='xx@xx.com' 这里填你自己邮箱地址。

root@instance-1:~/.acme.sh# ls  
account.conf acme.sh acme.sh.env acme.sh.log ca deploy dnsapi http.header notify vrain.cf  
root@instance-1:~/.acme.sh# vi ac  
root@instance-1:~/.acme.sh# vi account.conf

这一步做好了之后再申请

`[Thu Jul 29 01:28:33 UTC 2021] Add txt record error.  
[Thu Jul 29 01:28:33 UTC 2021] Error add txt for domain:_acme-challenge.XX.cf`

本以为大功告成，结果，又报错了。然后根据官方指引 加入 --debug 2 参数，

`"errors": [  
{  
"code": 1038,  
"message": "You cannot use this API for domains with a .cf, .ga, .gq, .ml, or .tk TLD (top-level domain). To configure the DNS settings for this domain, use the Cloudflare Dashboard."  
}  
],`

原来Cloudflare 的API 不技持 .cf, .ga, .gq, .ml, or .tk 的域名申请证书，汗，折腾半天。然后，换个域名，执行

`~/.acme.sh/acme.sh --issue --dns dns_cf -d fxx.com -d *.fxx.com`

OK了，API申请的好处，到期之后，直接再执行一下，上面命令就可以续期了，做个定时任务，不用担心证书过期。

看来..cf, .ga, .gq, .ml, or .tk这些域名，只能通过WEB认证申请了。本文就不讨论了。