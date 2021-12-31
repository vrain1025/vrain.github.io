---
title: Wp-PageNavi 使用
tags: []
id: '152'
categories:
  - - 未分类
date: 2011-07-19 17:28:33
---

1、把下载下来的文件解压，并将pagenavi（注意，pagenavi而不是wp-pagenavi文件）文件上传到/wp-content/plugins/目录下。

官方下载：[WP-pagenavi](http://wordpress.org/extend/plugins/wp-pagenavi/)

2、到后台的设置（optation）,在PageNavi下设置参数，英文版本的为：‘WP-Admin -> Options -> PageNavi’

3、最后，在你想要添加这个分页的地方加上如下的代码：

<?php if(function\_exists(‘wp\_pagenavi’)) { wp\_pagenavi(); } ?>

这样，就大功告成了！不过，如果你要达到更好的效果的话，那就么要设置一下插件的CSS文件。你可以用以下链接进行修改

/wp-content/plugins/pagenavi/pagenavi-css.css
要是自己不会改，在网上找别人改好了，DOWNLOAD下来就行了。