---
layout: post
title: 如何使用Sysprep准备Windows系统并使用自动应答
categories: Windows
description: 
keywords: Windows
---

在准备Windows欢迎界面之前，我们可以通过进入Sysprep来实现准备Windows

**目录**

* TOC
{:toc}
  

## 1. 进入Sysprep

在Windows安装欢迎界面输入Ctrl+Shift+F3来进入Sysprep。
如果已经过了OOBE欢迎界面创建过账户，可以手动进入Sysprep，记得要删除创建好的用户。
 
```
手动进入Windows System Preparation Tool
>>cd C:\Windows\System32\Sysprep
>>Sysprep
```

[1. Customize Windows 10 Audit Mode](https://www.tenforums.com/tutorials/3020-customize-windows-10-image-audit-mode-sysprep.html)  
[2. Custom Image Q&A](https://itectec.com/superuser/can-i-create-a-custom-recovery-image-for-windows-10-like-recimg-did-in-windows-8-1/)  

## 2. 安装你想要的软件
确保在Audit Mode之后，安装你想要的软件，例如Office, 浏览器等。  

## 3. 桌面文件设置
打开C:\Users\Default并将你想要的桌面快捷方式复制进去。新建用户将会从这个用户文件夹复制文件。

## 4. Windows SIM设置
这个时候，我们需要创建应答文件。
Windows ADK下载地址： <https://docs.microsoft.com/zh-cn/windows-hardware/get-started/adk-install>
  
[应答文件参考步骤](https://www.windowscentral.com/how-create-unattended-media-do-automated-installation-windows-10)  
[Windows 10 应答文件参考模板](https://www.windowsafg.com/win10x86_x64_uefi.html)  


