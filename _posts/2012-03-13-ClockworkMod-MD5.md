---
layout: post
title: ClockworkMod Recovery 恢复备份 MD5 mismatch 安全解决方案
categories: Android
description: MD5 mismatch
keywords: ClockworkMod
---

不需要ADB即可达到目的。  
建议工具：Notepad++  

首先，打开你储存备份位置。把里面文件计算出MD5值(好压 压缩软件内含有该工具，或使用HashTab)  

使用Notepad++打开nandroid.md5 (或者直接使用Windows内置记事本打开，不过看上去比较乱)
把看到的MD5修改好保存。  

删除.android_secure.img或.android_secure.vfat.tar  

然后就可以了。



