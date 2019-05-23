---
layout: post
title: SQL Server 多表查询
categories: SQL
description: SQL Server 多表查询
keywords: SQL Server
---

前几天开始研究维护SQL Server，因为学校自己的教育系统非常烂，而且他们公司维护客服也非常坑爹。所以我就开始研究自己维护SQL Server而不是一有事情就找他们付费弄。

**目录**

* TOC
{:toc}

## SQL 基本多表查询
数据库来源： [MSDN GitHub](https://github.com/microsoft/sql-server-samples) AdventureWorks2017


```sql
Select a.BusinessEntityID,b.EmailAddress,c.FirstName,c.LastName,a.JobTitle,d.PhoneNumber
FROM [AdventureWorks2017].[HumanResources].[Employee] as a,[AdventureWorks2017].[Person].[EmailAddress] as b, [AdventureWorks2017].[Person].[Person] as c,[AdventureWorks2017].[Person].[PersonPhone] as d
WHERE a.BusinessEntityID = b.BusinessEntityID and  b.BusinessEntityID = c.BusinessEntityID and c.BusinessEntityID = d.BusinessEntityID
Order by BusinessEntityID
```



