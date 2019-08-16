---
layout: post
title: SQL 复制表
categories: SQL
description: SQL 复制表
keywords: SQL Server
---

把dbo.student的表，复制为backup3


**目录**

* TOC
{:toc}

## SQL Table复制



```sql

/****** Script for SelectTopNRows command from SSMS  ******/
SELECT * into backup3
  FROM [excel].[dbo].[student]
```



