---
layout: post
title: SQL 无法使用Union如何解决
categories: SQL
description: SQL 无法使用Union如何解决
keywords: SQL Server
---

SQL 无法使用Union，显示错误


**目录**

* TOC
{:toc}

## SQL Union错误
SQL 中可以使用UNION这个命令，来将两个表合并且自动删除重复的数据。  
Union All则是只是合并，不删除重复数据。

错误提示：The data type ntext cannot be used as an operand to the UNION, INTERSECT or EXCEPT operators because it is not comparable.  

这是由于数据中确实存在ntext这个数据格式导致的，由于ntext已经被nvarchar取代，所以需要找到哪个数据是ntext。  
尝试各种办法发现，只有找到这个数据并转换为nvarchar才可以。  

## SQL Union查找数据格式
这里我们使用以下命令来对每个表进行查询
```sql

SELECT COLUMN_NAME,DATA_TYPE
FROM INFORMATION_SCHEMA.COLUMNS
WHERE TABLE_NAME='TableThatNeedToCheck';
```

## 修改数据格式
找到问题后通过以下方式即可实现使用Union
```sql
CAST(Table.Column AS nvarchar)
```




