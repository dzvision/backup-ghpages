---
layout: post
title: Windows开始菜单无响应
categories: Windows
description: 
keywords: Windows
---


**目录**

* TOC
{:toc}

之前遇到过Windows开始菜单点击无响应，最近又遇到开始菜单搜索无响应或多次重启才可以使用。
所以我将解决方法记录一下方便自己。


## 解决方案
实际上，无论是开始菜单点击无响应，还是搜索无法搜索，或出现搜索服务重启，都可以通过以下方法解决。
打开PowerShell
输入
```
Get-AppXPackage -AllUsers | Foreach {Add-AppxPackage -DisableDevelopmentMode -Register "$($_.InstallLocation)\AppXManifest.xml"}
```