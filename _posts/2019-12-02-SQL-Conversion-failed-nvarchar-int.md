---
layout: post
title: SQL出现Conversion failed nvarchar int
categories: SQL
description: 
keywords: SQL
---


**目录**

* TOC
{:toc}

## 序
Conversion failed when converting the nvarchar value 'abcdef' to data type int.

## 表中其中值存在abc和123
这是因为表中值有abc也有123导致无法转换。

例子
| HEADER1 | Column | HEADER3 | HEADER4 |
| ------- | :------ | :-----: | ------: |
| content | abc | content | content |
| content | bbc | content | content |
| content | 123 | content | content |
| content | 345 | content | content |


## 解决办法
原文：
```
SELECT pbi.[PID]
      ,pbi.[SN]
      ,pbi.[FN]
      ,pbi.[G]
      ,pbi.[F]
      ,pbi.[YG]
      ,pbi.[H]
      ,pbi.[PS]
      ,pbi.[AN]
	  ,um.PUID, um.UN,ulh.IPA,ulh.LDate
  FROM [TestingTable].[dbo].[View_ContactDetail] as pbi
 Left join UserMaster um on pbi.AN=um.PUID 
 LEFT JOIN [UserLoginHistory] ulh on um.PUID = ulh.PUID AND ulh.LoginNumber = 1
 WHERE um.PUID is not null
```   

添加排除abc字母   
```sql
and um.PortalUserID not like '%[^0-9]%'
```

修改后   
```
SELECT pbi.[PID]
      ,pbi.[SN]
      ,pbi.[FN]
      ,pbi.[G]
      ,pbi.[F]
      ,pbi.[YG]
      ,pbi.[H]
      ,pbi.[PS]
      ,pbi.[AN]
	  ,um.PUID, um.UN,ulh.IPA,ulh.LDate
  FROM [TestingTable].[dbo].[View_ContactDetail] as pbi
 Left join UserMaster um on pbi.AN=um.PUID and um.PortalUserID not like '%[^0-9]%'
 LEFT JOIN [UserLoginHistory] ulh on um.PUID = ulh.PUID AND ulh.LoginNumber = 1
 WHERE um.PUID is not null
```    