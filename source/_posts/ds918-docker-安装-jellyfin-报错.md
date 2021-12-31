---
title: DS918+ docker 安装 jellyfin 报错
tags: []
id: '908'
categories:
  - - 个人原创
date: 2020-04-17 09:23:01
---

在jellyfin更新到新版本后，如果你是新装的话，你会发装，按正常流程设置好jellyfin 后进入到网页进行配置时，会报错。

There was an error processing the request. Please try again later.

出现上面那个错误是因为在安装时系统没有创建metadata文件夹，解决方法很简单，直接在你设置的config 文件夹下创建一个 metadata 文件夹就好了。我是直接在主目录下建了一个metadata。然后在系统设置中选择了这个文件夹。

![](https://gcsee.com/wp-content/uploads/2020/04/2020041709095264.png)

![](https://gcsee.com/wp-content/uploads/2020/04/2020041709081967-1024x501.png)

然后，你会发现转码也开启不了，会提示错误，前提是你已经以最高执行权限运行了容器。

这个解决方法也是一样，在config文件夹下创建transcodes文件夹，在上面文件夹截图里我已经截图了，这里就不再详细写了。然后，就可以开启转码，下面是转码演示。

![](https://gcsee.com/wp-content/uploads/2020/04/2020041709223184-1024x418.gif)