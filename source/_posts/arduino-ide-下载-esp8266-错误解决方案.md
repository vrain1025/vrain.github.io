---
title: arduino IDE 下载 esp8266 错误解决方案
tags: []
id: '934'
categories:
  - - 个人原创
date: 2020-10-13 09:43:15
---

如果你遇到

![](https://gcsee.com/wp-content/uploads/2020/10/c11013.jpg)

下载 https://arduino.esp8266.com/stable/package\_esp8266com\_index.json 时出错

或者下载 http://arduino.esp8266.com/stable/package\_esp8266com\_index.json 时出错

不是你的问题，这是这个网站上存的这个文件没有了，我试了，HTTP和HTTPS都无法打开这个文件，所以如果你想安装最新的ESP8266的开发插件，可以直接到[https://github.com/esp8266/Arduino/](https://github.com/esp8266/Arduino/) 然后点击[Release](https://github.com/esp8266/Arduino/releases/tag/2.7.4)，里面有各版本的ESP8266 arduino开发插件。找到最新版本里面有个json文件，在首选项里添加这个json文件的地址，就可以像原来一样在开发板管理器里安装这个插件了。（有个前提，就是你能打开并下载github里的文件），如果你打不开github，你就用国内的那个安装包。直接安装这个安装包吧，这个不是最新版的。[https://pan.baidu.com/s/1BGT9Vw31mz5CdlPKyKYXUQ](https://pan.baidu.com/s/1BGT9Vw31mz5CdlPKyKYXUQ) **（提取码：49c1）**

![](https://gcsee.com/wp-content/uploads/2020/10/2020-10-13_093659.jpg)

![](https://gcsee.com/wp-content/uploads/2020/10/2020-10-13_093734.jpg)