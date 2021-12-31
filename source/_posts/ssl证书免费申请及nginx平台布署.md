---
title: SSL证书免费申请及nginx平台布署
tags: []
id: '558'
categories:
  - - 个人原创
date: 2016-09-18 17:40:48
---

最近发现越来越多的网站开始采用HTTPS连接，查了一下原因。

> HTTP协议有一个缺陷，它在传输过程中的数据包是明文的，这对于网上交易等需要数据保密的操作来说，是致命的。在这种需求下，促使越来越多的网站使用https协议进行数据传输。

> 为什么需要HTTPS？ HTTP全名超文本传输协议，它是网络应用广泛使用的协议，客户端据此获取服务器上的超文本内容。客户端包括浏览器、PC软件客户端以及大部分手机App。超文本内容则以HTML为主，客户端拿到HTML内容后可根据规范进行解析呈现。因此，HTTP主要负责的是“内容的请求和获取”。 问题就出在这部分。内容请求和获取时会经过许多中间人，主要是网络环节，充当内容入口的浏览器、路由器厂商、WIFI提供商、通信运营商，如果使用了代理、翻墙软件则会引入更多中间人。由于HTTP请求的路径、参数默认情况下均是明文的，因此这些中间人可以对HTTP请求进行监控、劫持、阻挡。一些关键参数比如登录密码开发者会在客户端进行MD5加密，不过互联网所承载的机密信息远不只是密码，搜索内容同样属于敏感信息。 在没有HTTPS时，运营商可在用户发起请求时直接跳转到某个广告，或者直接改变搜索结果插入自家的广告。浏览器和安全软件可以监听用户搜索在结果页植入广告。一些中间人还可把用户数据直接转卖，这样你搜索了“保险”以后你就成了保险公司电话推销的目标。如果劫持代码出现了BUG，则直接让用户无法搜索，出现白屏。 不只是搜索引擎，其他的网络应用同样会面临这些问题：数据泄露、请求劫持、内容篡改等等，核心原因就在于HTTP是全裸式的明文请求，域名、路径和参数都被中间人们看得一清二楚。HTTPS做的就是给请求加密，让其对用户更加安全。对于自身而言除了保障用户利益外，还可避免本属于自己的流量被挟持，以保护自身利益。 尽管HTTPS并非绝对安全，掌握根证书的机构、掌握加密算法的组织同样可以进行中间人形式的攻击。不过HTTPS是现行架构下最安全的解决方案，并且它大幅增加了中间人攻击的成本。

既然HTTPS是以后的趋势，那么我们就跟随趋势，加入HTTPS的队伍吧。 1.申请SSL证书 先说一下证书的分类

> 域名型SSL证书（DV SSL） ，即只对域名的所有者（一般是域名管理员邮箱，比如admin@hotmail.com）进行在线检查，具体是发送验证邮件给域名管理员或以该域名结尾的邮箱至于该域名的管理员是真实注册的单位还是另有其人，就不得而知了。 企业型 SSL 证书（OV SSL） ，是要购买者提交组织机构资料和单位授权信等在官方注册的凭证，认证机构在签发SSL证书前不仅仅要检验域名所有权，还必须对这些资料的真实合法性进行多方查验，只有通过验证的才能颁发SSL证书。 增强型 SSL 证书（EV SSL） ，与其他SSL证书一样，都是基于SSL/TLS安全协议，都是用于网站的身份验证和信息在网上的传输加密。它跟普通SSL证书的区别也是明显的，安全浏览器的地址栏变绿，如果是不受信的SSL证书则拒绝显示，如果是钓鱼网站，地址栏则会变成红色，以警示用户。

免费申请证书的网站很多，下面是在网上看到的。 https://freessl.wosign.com/ （推荐这一个，申请简单，申请完，证书有效期3年，现在已经停止申请了） https://www.zzidc.com/main/ssl/showmianfei.html https://cloud.baidu.com/product/cas.html https://console.qcloud.com/ http://wangzhan.360.com/ 国外 https://www.ssllabs.com/ssltest/ https://aws.amazon.com/cn/blogs/aws/new-aws-certificate-manager-deploy-ssltls-based-apps-on-aws/ https://ssl.uk2.net/cgi-bin/retrieve-certificate.pl https://ssl.uk2.net/cgi-bin/certificate-apply.pl https://www.cloudflare.com/ https://www.startssl.com/ （现在推荐这个） https://www.sslforfree.com/ https://certbot.eff.org/ https://letsencrypt.org/ https://github.com/Vittfarne/ASSL https://assl.loovit.net/

* * *

下面以startssl为例生成key 文件 在服务器中运行： openssl req -newkey rsa:2048 -keyout yourname.key -out yourname.csr ![](http://gcsee.com/wp-content/uploads/2016/09/2017-03-22_143627-375x250.png) vi yourname.csr 将CSR文件内容复制出来，填在申请位置 2.将证书上传到服务器，必添加相关服务器配置内容，以nginx为例。

server
    {
        listen 443;
        ssl on;
        ssl\_certificate /usr/local/nginx/ssl/这里改成你自己的证书名.crt;
        ssl\_certificate\_key /usr/local/nginx/ssl/这里改成你自己的KEY名.key;
        ssl\_session\_timeout 24h;
        keepalive\_timeout 300s;
    }

3.若想将HTTP的请求，跳转到HTTPS上的话，可以在HTTP的SERVER配置下面加一条301跳转。

server
    {
        listen 80;
        #listen \[::\]:80;
        return 301 https://$server\_name$request\_uri;
}