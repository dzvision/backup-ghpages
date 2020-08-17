---
layout: post
title: SQL如何对不同表的数据进行更新
categories: SQL
description: 
keywords: SQL
---

如果我们有表A和表B, 我想把我的表A的Col1内的数据更新到表B的Col1里面，那么我们怎么做呢？

**目录**

* TOC
{:toc}


## Microsoft SQL例子
```
UPDATE        scores
SET           scores.name = p.name
FROM          scores s
INNER JOIN    people p
ON            s.personId = p.id
```  

## MySQL例子
```
UPDATE    scores s,
          people p
SET       scores.name = people.name
WHERE     s.personId = p.id
```  



## 参考文献
1. [TravisHorn](https://travishorn.com/update-from-another-table-in-sql-382507f9ff6a)
