---
layout: post
title: Proxifier Reset Tool
categories: 随笔
description: 无限重置Proxifier
keywords: Proxifier
---

Proxifier如何实现无线重置试用期呢？



### 1. 编辑bat文件

```
REM Initex Software Proxifiertrial reset
REM Close Proxifier if it is running
taskkill /f /im Proxifier.exe

reg delete "HKCU\SOFTWARE\Microsoft\Internet Explorer\Main" /v DefaultWANProfile /f
reg delete "HKCU\Software\Initex\ProxyChecker\Settings" /v DefaultWANProfile /f
reg delete "HKCU\Software\Initex\Proxifier\Settings" /v DefaultWANProfile /f

REM Delete "DefaultWANProfile" line in "Settings.ini" file in ProxifierPE folder (for Portable Edition)
del %~dp0Settings.old.ini
ren %~dp0Settings.ini Settings.old.ini
type %~dp0Settings.old.ini | findstr /v DefaultWANProfile > %~dp0Settings.ini 
```
实际上本文后半段不需要复制，只需要直接删除文件即可。  

### 2. 放入到Proxifier目录文件夹内

### 3. 删除目录文件夹内的Setting.ini和Profile文件夹 (完成)
