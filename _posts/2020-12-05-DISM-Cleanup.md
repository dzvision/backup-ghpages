---
layout: post
title: 通过DISM清理组件储存文件
categories: Windows
description: 
keywords:Windows
---

我们知道WinSxS是一个在C盘无法删除的重要系统文件，那么我们如何给他瘦身呢？

**目录**

* TOC
{:toc}
  

## PowerShell清理

 
```
PS C:\WINDOWS\system32> Dism.exe /Online /Cleanup-Image /AnalyzeComponentStore

部署映像服务和管理工具
版本: 10.0.18362.1139

映像版本: 10.0.18363.1198

[==========================100.0%==========================]

组件存储(WinSxS)信息:

Windows 资源管理器报告的组件存储大小 : 7.34 GB

组件存储的实际大小 : 6.96 GB

    已与 Windows 共享 : 4.33 GB
    备份和已禁用的功能 : 2.63 GB
    缓存和临时数据 :  0 bytes

上次清理的日期 : 2020-11-30 19:36:17

可回收的程序包数 : 1
推荐使用组件存储清理 : 是

操作成功完成。
PS C:\WINDOWS\system32> DISM.exe /online /Cleanup-Image /StartComponentCleanup

部署映像服务和管理工具
版本: 10.0.18362.1139

映像版本: 10.0.18363.1198

[=====                      10.0%                          ]
[==========================100.0%==========================]
操作成功完成。
PS C:\WINDOWS\system32> Dism.exe /Online /Cleanup-Image /AnalyzeComponentStore

部署映像服务和管理工具
版本: 10.0.18362.1139

映像版本: 10.0.18363.1198

[==========================100.0%==========================]

组件存储(WinSxS)信息:

Windows 资源管理器报告的组件存储大小 : 5.43 GB

组件存储的实际大小 : 5.40 GB

    已与 Windows 共享 : 4.27 GB
    备份和已禁用的功能 : 1.13 GB
    缓存和临时数据 :  0 bytes

上次清理的日期 : 2020-12-02 06:42:51

可回收的程序包数 : 0
推荐使用组件存储清理 : 否
```