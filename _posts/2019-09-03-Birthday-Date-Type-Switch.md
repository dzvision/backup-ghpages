---
layout: post
title: SQL生日问题排查及调整
categories: SQL
description: 
keywords: SQL Server
---

## SQL生日问题排查及调整

**目录**

* TOC
{:toc}

## Excel 生日格式严重不一致导致导入发生问题
在发现部分数据库中的生日数据与导入表实际上是不一致的错误，通过怎么样的方式来实现查询并修正呢？  
因为我们部分数据日与月相反，我们想要通过导入前的那张招生表来查出差别。  
实际操作中，Excel无法完美识别出日期，导致无法对比。  

## 多表合并对比
SQL命令里面我们根据网上
select CONVERT (varchar(23), getdate(), 121)
也无法得到我们想要的YYYY-MM-DD HH:MM:SS.000 格式
因为我们SQL数据库的数据是datetime的形式储存的（不是varchar)。
我们也尝试使用Select Concat(a,b)的形式合并时间。（即把招生表的2012-04-15,新建00:00:00.000,并合并成一个）
结果也不满意。



## 最终方法
实际上，最好的方式还是

SELECT PARSE('21/11/2014' AS datetime USING 'it-IT')

也就是
SELECT PARSE(你的表.你的字段col AS datetime USING 'it-IT')
这样才是最好的方式。

## 后语
实际上，多表查询并不能查询出生日中的“日/月”对换错误，因为在原表中，就已经是错误的了。所以在使用Excel中调整日期的格式一定要十分注意，免得他之调整了一部分。
然后我们再也不知道哪些是对的，哪些是错的。