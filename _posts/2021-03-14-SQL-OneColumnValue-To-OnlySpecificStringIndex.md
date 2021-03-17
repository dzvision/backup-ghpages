---
layout: post
title: SQL中如何将一列中的值显示出字符指定位置与指定长度。
categories: SQL
description: 
keywords: SQL
---

我们在对比系统目前存在的生日与身份证的时候会问，怎么只取其中值的特定位置，获得对比结果。
例如我们有一个值是123456789,那么我们怎么只显示4567呢？  



**目录**

* TOC
{:toc}



## 示例
```sql
SELECT 
	... ...
	,convert(varchar, table1.[BirthDate], 112) as SystemBD
	,substring(table2.ResidentialID,7,8) AS RBD
From Database1
Where SystemBD != RBD AND table2.ResidentialID like '__________________'
```

我们可以参考[w3schools](https://www.w3schools.com/sql/func_sqlserver_substring.asp)的介绍。
也就是，从身份证第7位起，长度为8位。注意，他和程序中的index不一样，开始第一个字符就是1，而不是0。
