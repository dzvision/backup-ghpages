---
layout: post
title: Windows Server 如何把评估版本改变为正式版本
categories: 服务器
description: 
keywords: Server
---

## Windows Server评估版修改为正式版

**目录**

* TOC
{:toc}

## 下载Windows Server
有的时候，直接从微软下载会快很多，但是因为从微软下载，它的版本都是评估版，那么我们怎么修改版本呢？

## 1. 运行cmd
开始————运行————CMD(管理员模式) 
输入：   
```
DISM /online /Get-CurrentEdition
```
查看看你的 Edition ID 是什么，
如果是 Evaluation 的话，例如 Standard 标准版评估版本，一般就是
ServerStandardEval 把后面 Eval 那四字母去了就是你的 Edition ID。
例如ServerStandardEval的就是改为ServerStandard
ServerDatacenterEval也是同理

## 2. 转换版本
然后输入
DISM /online /Set-Edition: /ProductKey:XXXXX-XXXXX-XXXXX-XXXXX-XXXXX /AcceptEula  
  
Edition ID 自己填刚才得到的那个，ProductKey 后面把序列号填上去就行。  

你也可以通过这个方式把Standard版本改为Datacenter版。

## 3. 重启操作系统
  


### 激活码
Retail V6WN6-YBX49-KPV7T-TFVB2-XTRB4  
Retail XMTCT-M3NTG-2K764-CYDHX-XK2JF  
Retail NPTRB-CFYFD-DGFPG-DY9GJ-CPR8F  
Retail 4NM38-4K89B-MWMFG-2M9YM-43PJF  
Retail 76WDM-TN9D3-JTBH4-FCR4R-3DDFR  
Retail	8KQ9N-H2TQK-39DHB-9RCD8-9TRB4  
Retail	9YDXY-4N3FG-8RBT3-JC8B3-VXQFR  
Retail	BV7D6-NDRFX-TYDH6-8YBQV-DRVY4  
Retail	F93BG-2NQGW-3FKT3-7P8MK-3RVY4  
Retail	KM4GN-DQFRK-DXYDC-MVWPX-PBBM4  
Retail	NFJ77-RMF62-V89VY-G4B7Y-VQYM4  
Retail	FKNJR-W7HW8-3GX3R-7YVGY-6VMM4  
GVLK	WMDGN-G9PQG-XVVXX-R3X43-63DFG  
Retail	G74NR-DYWGM-979TC-8Y79P-XTRB4  
Retail	YPFKW-TKNDC-YF636-CQTPW-Q7CJF  
Retail	W6CJW-NTXD6-KQKGC-48CVV-BDYM4  