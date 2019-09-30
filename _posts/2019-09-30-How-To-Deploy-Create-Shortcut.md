---
layout: post
title: Windows如何在不加入域环境的局域网内分发软件以及如何创建快捷方式
categories: Windows
description: 
keywords: Windows Deployment
---

## WWindows如何在不加入域环境的局域网内分发软件以及如何创建快捷方式

**目录**

* TOC
{:toc}

## 下载PDQ Deploy
这个软件是最好的选择。  
虽然我曾经想过使用metasploit,boxstarter等方式分发，最后发现，这个最简单。  

## 在PDQ Deploy里使用命令
exe格式的文件需要根据封装方式来查看他的静默安装命令，常见的有
```
#1
/slient /install

#2
/S

#3
/quiet /passive
等等
```
我们通过静默软件工具查看并猜测出静默安装的命令


## 快捷方式
部分软件安装之后，并不会全局用户上创建快捷方式， 我们可以通过以下方式实现。
  
```
echo Set oWS = WScript.CreateObject("WScript.Shell") > CreateShortcut.vbs
echo sLinkFile = "C:\Users\a1\Desktop\ShortcutToSource.lnk" >> CreateShortcut.vbs
echo Set oLink = oWS.CreateShortcut(sLinkFile) >> CreateShortcut.vbs
echo oLink.TargetPath = "D:\test\RealLocation.exe" >> CreateShortcut.vbs
echo oLink.Save >> CreateShortcut.vbs
cscript CreateShortcut.vbs
del CreateShortcut.vbs
```

高阶版  
```
@echo off

set SCRIPT="%TEMP%\%RANDOM%-%RANDOM%-%RANDOM%-%RANDOM%.vbs"

echo Set oWS = WScript.CreateObject("WScript.Shell") >> %SCRIPT%
echo sLinkFile = "%USERPROFILE%\Desktop\myshortcut.lnk" >> %SCRIPT%
echo Set oLink = oWS.CreateShortcut(sLinkFile) >> %SCRIPT%
echo oLink.TargetPath = "D:\myfile.extension" >> %SCRIPT%
echo oLink.Save >> %SCRIPT%

cscript /nologo %SCRIPT%
del %SCRIPT%
```

