---
layout: post
title: SQL 如何将表中行列互换
categories: SQL
description: SQL 行列互换
keywords: SQL Server
---

在工作中，我们发现有时候需要将表中的行列进行互换。


**目录**

* TOC
{:toc}

## SQL 列换成行
SQL 中可以使用PIVOT这个命令，同理，行换成列使用UNPIVOT。

```sql

SELECT * FROM 
(SELECT [StudentID]
      ,[Surname]
      ,[ForeName],[YearGroup]
	  ,[Class]
      ,[SubjectName]
	  --,[SubjectChineseName]
      ,CAST([StudentMarkData] AS float) AS Mark2
  FROM [newDB].[dbo].[ClassMarksheet]
  ) AS BaseTable
  PIVOT( 
	AVG(Mark2)
	FOR [SubjectName] in ([Mathematics],[Chinese],[English],[Science])
) AS StudentMarksMerge
```
使用PIVOT需要注意的是，必须把其他列中同一学生不同信息列隐藏才可以。  
例如：我们把一行一行列出的科目变成一列一列，我们的SubjectChineseName就要隐藏掉，否则Pivot出来的结果是同一个学生一样有四行。  
只不过右边多出了四列科目而已。
我这里先CAST是因为需要转换格式，从NVARCHAR转为FLOAT。  
如果我想要转换的行列数据不是数字的话，应该用什么？
我们可以通过COUNT得到出现的次数，也可以通过MIN()或者MAX()直接显示内容。



