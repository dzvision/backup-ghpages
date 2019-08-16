---
layout: post
title: SQL Server 手机类型更新
categories: SQL
description: SQL Server 手机类型更新
keywords: SQL Server
---

我们有的时候会遇到整体数据类型更变的需求。  
例如本来我的手机类型原本是“家用”，要修改成“工作”。  
在数据中，手机类型，往往是直接UID类型来表示，或者简单的用1，2，3来标识。  
以下就是当手机类型修改从2，3，都修改为1的方法。


**目录**

* TOC
{:toc}

## SQL 手机类型更新
数据库来源： [MSDN GitHub](https://github.com/microsoft/sql-server-samples) AdventureWorks2017


```sql
UPDATE [Person].[PersonPhone]
Set PhoneNumberTypeID = Case
							When PhoneNumberTypeID = '2' THEN '1'
							When PhoneNumberTypeID = '3' THEN '1'
							ELSE PhoneNumberTypeID
						END
WHERE PhoneNumberTypeID IN ('2','3')


SELECT *
FROM [AdventureWorks2017].[Person].[PersonPhone]
```



