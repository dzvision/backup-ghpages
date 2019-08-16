---
layout: post
title: SQL 把一个表内字段的值复制到另一个表内的特定字段
categories: SQL
description: SQL 把一个表内字段的值复制到另一个表内的特定字段
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



