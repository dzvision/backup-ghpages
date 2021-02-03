---
layout: post
title: SQL如何将一个列中值内的逗号分割成另一列
categories: SQL
description: 
keywords: SQL
---

有时候，我们会想将一个列中的值分成多列。


**目录**

* TOC
{:toc}



## 示例
例如某个列是这样的：
7890 – 20th Ave E Apt 2A, Seattle, VA  
9012 W Capital Way, Tacoma, CA  
5678 Old Redmond Rd, Fletcher, OK  
3456 Coventry House Miner Rd, Richmond, TX  


## 代码
[1. MS SQL Tips](https://www.mssqltips.com/sqlservertip/6321/split-delimited-string-into-columns-in-sql-server-with-parsename/)    


```sql
SELECT 
     REVERSE(PARSENAME(REPLACE(REVERSE(myAddress), ',', '.'), 1)) AS [Street]
   , REVERSE(PARSENAME(REPLACE(REVERSE(myAddress), ',', '.'), 2)) AS [City]
   , REVERSE(PARSENAME(REPLACE(REVERSE(myAddress), ',', '.'), 3)) AS [State]
FROM dbo.custAddress
```

## 结果：
| Street | City | State |
| ------ | ------ | ------ | 
| 7890 – 20th Ave E Apt 2A | Seattle | VA |
| 9012 W Capital Way | Tacoma | |CA |  
