---
layout: post
title: Excel 如何将表中行列互换
categories: Excel
description: Excel 行列互换
keywords: Excel
---

在工作中，我们发现有时候需要将表中的行列进行互换。之前我们讲了SQL中的操作，那么如果是Excel如何实现呢？


**目录**

* TOC
{:toc}

## Excel中使用Power Query实现

Step 1: 首先，我们先进入Data --> From Table/Range 选好区域回车。
![Step1](/blog/images/posts/2020/20200924_Excel_Transpose_Step1)

Step 2:  
![Step2](/blog/images/posts/2020/20200924_Excel_Transpose_Step2)

然后我们选中把行变成列的那一整列，再去Transform --> Pivot Column

Step 3:
Values Column选择成绩，而Advanced Options无需看，无论是SUM还是AVG结果都一样的。

## Excel中使用Pivot Table去做
（个人觉得这个不太好用）
从Insert找到Pivot Table即可。
