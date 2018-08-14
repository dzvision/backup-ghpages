---
layout: post
title: 修改系统初始安装时间
categories: Windows
description: Windows 安装时间修改
keywords: Windows
---

修改系统安装时间
开始" - "运行" - 输入"regedit" - 回车，依次找到以下路径

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion


右侧的 InstallDate 就是微软保存"初始安装日期"的键值，可以通过以 十进制 方式更改UNIX时间戳来更改这个时间


UNIX时间戳十进制转换：
http://tool.chinaz.com/Tools/unixtime.aspx


