---
title: office 2010 去除启动界面
tags: []
id: '362'
categories:
  - - 未分类
date: 2012-03-21 10:07:23
---

office 2010 的启动速度真的比以前慢了好多，然后想着去掉启动界面会不会变快点呢，在网上查了很久，今天无意中在远景论坛看到有人的方法，经测试的确可以去掉启动界面，不过，去掉启动界面启动速度是不会变快的，这就跟WINDOWS 启动一个道理，就算没有那进度条它还是在加载，只是掩耳盗铃罢了。不过方法还是分享给有需要的人，导入如下文件到注册表就行了，建议先备份，省得你到时候想恢复就麻烦了。

Windows Registry Editor Version 5.00
;FOR X86
;word:
\[HKEY\_CLASSES\_ROOT\\Word.Document.12\\shell\\Open\\command\]
@="\\"C:\\\\Program Files\\\\Microsoft Office\\\\Office14\\\\WINWORD.EXE\\" /p /n \\\\\\"%1\\\\\\""
"command"=hex(7):78,00,62,00,27,00,42,00,56,00,35,00,21,00,21,00,21,00,21,00,\\
  21,00,21,00,21,00,21,00,21,00,4d,00,4b,00,4b,00,53,00,6b,00,57,00,4f,00,52,\\
  00,44,00,46,00,69,00,6c,00,65,00,73,00,3e,00,62,00,69,00,24,00,54,00,21,00,\\
  56,00,21,00,30,00,5a,00,3d,00,7b,00,50,00,6b,00,30,00,76,00,6d,00,7e,00,41,\\
  00,5a,00,75,00,2f,00,71,00,20,00,2f,00,6e,00,20,00,22,00,25,00,31,00,22,00,\\
  00,00,00,00
;---------------------------
;Excel:
\[HKEY\_CLASSES\_ROOT\\Excel.Sheet.12\\shell\\Open\\command\]
@="\\"C:\\\\Program Files\\\\Microsoft Office\\\\Office14\\\\EXCEL.EXE\\" /e /dde"
"command"=hex(7):78,00,62,00,27,00,42,00,56,00,35,00,21,00,21,00,21,00,21,00,\\
  21,00,21,00,21,00,21,00,21,00,4d,00,4b,00,4b,00,53,00,6b,00,45,00,58,00,43,\\
  00,45,00,4c,00,46,00,69,00,6c,00,65,00,73,00,3e,00,56,00,69,00,6a,00,71,00,\\
  42,00,6f,00,66,00,28,00,59,00,38,00,27,00,77,00,21,00,46,00,49,00,64,00,31,\\
  00,67,00,4c,00,51,00,20,00,2f,00,65,00,20,00,2f,00,64,00,64,00,65,00,00,00,\\
  00,00
;---------------------------
;PowerPoint:
\[HKEY\_CLASSES\_ROOT\\PowerPoint.Show.12\\shell\\Open\\command\]
@="\\"C:\\\\Program Files\\\\Microsoft Office\\\\Office14\\\\POWERPNT.EXE\\" \\"%1\\" /s"
"command"=hex(7):78,00,62,00,27,00,42,00,56,00,35,00,21,00,21,00,21,00,21,00,\\
  21,00,21,00,21,00,21,00,21,00,4d,00,4b,00,4b,00,53,00,6b,00,50,00,50,00,54,\\
  00,46,00,69,00,6c,00,65,00,73,00,3e,00,6c,00,35,00,59,00,41,00,73,00,68,00,\\
  4a,00,35,00,65,00,39,00,3f,00,51,00,31,00,30,00,60,00,46,00,46,00,63,00,32,\\
  00,43,00,20,00,22,00,25,00,31,00,22,00,20,00,2f,00,73,00,00,00,00,00

.csharpcode, .csharpcode pre { font-size: small; color: black; font-family: consolas, "Courier New", courier, monospace; background-color: #ffffff; /\*white-space: pre;\*/ } .csharpcode pre { margin: 0em; } .csharpcode .rem { color: #008000; } .csharpcode .kwrd { color: #0000ff; } .csharpcode .str { color: #006080; } .csharpcode .op { color: #0000c0; } .csharpcode .preproc { color: #cc6633; } .csharpcode .asp { background-color: #ffff00; } .csharpcode .html { color: #800000; } .csharpcode .attr { color: #ff0000; } .csharpcode .alt { background-color: #f4f4f4; width: 100%; margin: 0em; } .csharpcode .lnum { color: #606060; }