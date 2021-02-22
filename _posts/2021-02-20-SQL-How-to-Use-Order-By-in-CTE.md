---
layout: post
title: SQL如何在CTE中使用Order By的功能
categories: SQL
description: 
keywords: SQL
---

我们知道，CTE是不可以使用Order BY的，那么我们有什么方法可以通过类似方法实现Order By的功能呢？


**目录**

* TOC
{:toc}



## 示例
```sql
With Base AS (

SELECT 
	... ...
From Database1

--T1 根据Base.SID排序

T1 AS (
Select *,rn = ROW_NUMBER() Over (Order By Base.SID) 
From Base),
```