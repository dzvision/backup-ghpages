---
layout: post
title: SQL 把一个表内字段的值复制到另一个表内的特定字段
categories: SQL
description: SQL 把一个表内字段的值复制到另一个表内的特定字段
keywords: SQL Server
---

如果我们想要把一个表内某个字段的值，复制到另一个表内的另一个字段，那么我们怎么做呢？  
假如我们想把a表的EmailAddress替换为b表的PasswordHash,
那么我们可以基于BusinessEntityID来识别每一行来进行匹配并更变数值。


**目录**

* TOC
{:toc}

## SQL 手机类型更新
数据库来源： [MSDN GitHub](https://github.com/microsoft/sql-server-samples) AdventureWorks2017


```sql
Update a
Set a.EmailAddress = b.PasswordHash
FROM [AdventureWorks2017].[Person].[EmailAddress] as a,[AdventureWorks2017].[Person].[Password] as b
WHERE a.BusinessEntityID = b.BusinessEntityID
```



