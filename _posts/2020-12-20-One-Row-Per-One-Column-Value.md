---
layout: post
title: SQL如何只让特定列中只显示一行数据
categories: SQL
description: 
keywords: SQL
---

我们如果在某个表里面，如何让其中某列的其中一行数据，只是显示一次呢？

**目录**

* TOC
{:toc}


## 示例表

| StudentID | Last_Name | First_Name | Gender | GradeLevel | Class | Pupil_Email	| Relationship |	Pupil_Parent_Email |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| 5013 |	Wang |	Zack | M |	Grade 9 Senior |	SG9 B |	5013@example.com |	爸爸 |	aaa@qq.com |
| 5013 |	Wang |	Zack |	M |	Grade 9 Senior |	SG9 B |	5013@example.com |	妈妈 |	bbb@qq.com |
| 5014 |	Liu |	Aileen |	F |	Grade 2 Bilingual	 | BG2 D | 	5014@example.com |	爸爸	 | ccc@tt.com |
| 5014 |	Liu |	Aileen |	F |	Grade 2 Bilingual	 | BG2 D | 	5014@example.com | 妈妈 | ddd@gg.com |
| 5014 |	Liu |	Aileen |	F |	Grade 2 Bilingual	 | BG2 D | 	5014@example.com | 妈妈 |extra-email@gg.com |
| 5017 |	Ying | 	Eason | 	F | 	Grade 9 Senior | 	SG9 A |	5017@example.com |	爸爸	| e@e.com | 
| 5017 |	Ying | 	Eason | 	F | 	Grade 9 Senior | 	SG9 A |	5017@example.com |	爸爸	| e@e.com | 
| 5029	| Yan	| Yuki	| M	| Grade 3 Bilingual	| BG3 H	| 5029@example.com	| 爸爸	| f@f.com | 
| 5029	| Yan	| Yuki	| M	| Grade 3 Bilingual	| BG3 H	| 5029@example.com	| 妈妈 | g@g.com | 
| 5029	| Yan	| Yuki	| M	| Grade 3 Bilingual	| BG3 H	| 5029@example.com	| 妈妈 | 2@g.com |
| 5029	| Yan	| Yuki	| M	| Grade 3 Bilingual	| BG3 H	| 5029@example.com	| 妈妈 | 3@g.com |

## 解析
如你所见，学号5014和5029的学生妈妈出现多次，而5017学生同样数据显示了2次。那么我们如何让其数据，也就是“妈妈”，只显示其中一个呢?

## Step 1 DISTINCT
DISTINCT是可以将重复数据去除，只显示一行。但是这个是全部Select表的重复数据。所以如果想要“妈妈”信息只是显示一条是不可行的。
我们先将5017学生的重复数据去除


## Step 2 MIN()和Group By 
我们将想要只显示一条数据的列进行MIN()或MAX() 【根据字母大小显示第一条】
Group By后面跟着所有除去MIN()那一列的数据即可。

```sql
Select DISTINCT
StudentID
,Last_Name
,First_Name
,Gender
,GradeLevel
,Class
,Pupil_Email
,Relationship
,MIN(Pupil_Parent_Email) AS Pupil_Parent_Email

From TableA

Group By StudentID
,Last_Name
,First_Name
,Gender
,GradeLevel
,Class
,Pupil_Email
,Relationship

```

结果：  

| StudentID | Last_Name | First_Name | Gender | GradeLevel | Class | Pupil_Email	| Relationship |	Pupil_Parent_Email |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| 5013 |	Wang |	Zack | M |	Grade 9 Senior |	SG9 B |	5013@example.com |	爸爸 |	aaa@qq.com |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| 5013 |	Wang |	Zack |	M |	Grade 9 Senior |	SG9 B |	5013@example.com |	妈妈 |	bbb@qq.com |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| 5014 |	Liu |	Aileen |	F |	Grade 2 Bilingual	 | BG2 D | 	5014@example.com |	爸爸	 | ccc@tt.com |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| 5014 |	Liu |	Aileen |	F |	Grade 2 Bilingual	 | BG2 D | 	5014@example.com | 妈妈 | ddd@gg.com |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| 5017 |	Ying | 	Eason | 	F | 	Grade 9 Senior | 	SG9 A |	5017@example.com |	爸爸	| e@e.com | 
| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| 5029	| Yan	| Yuki	| M	| Grade 3 Bilingual	| BG3 H	| 5029@example.com	| 爸爸	| f@f.com | 
| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| 5029	| Yan	| Yuki	| M	| Grade 3 Bilingual	| BG3 H	| 5029@example.com	| 妈妈 | 2@g.com |


上面我们所有的工作已经完成了！如果我想要将该表的邮箱行列进行互换呢？  
如果想要互换，当然可以直接通过PIVOT来实现，但是如果我们想要先计算学生有多少个长辈邮箱，且每个长辈邮箱只显示一个，我们应该怎么做呢？


## Step 3 ROW_NUMBER()


[SQL Server Tutorial ROW_NUMBER()教学](https://www.sqlservertutorial.net/sql-server-window-functions/sql-server-row_number-function/)  
我们可以根据父母关系邮箱来进行排序

以下是基本用法
```
ROW_NUMBER() OVER (
Order By TableA.ColumnID
) AS Count_Row_No
```

通过上面的方式，只是计算总数的行数(Row Number), 在实际使用中，我们更多是根据某一列的数据来计算他的数据出现的次数。  
例如：
```
ROW_NUMBER() OVER (
PARTITION By TableA.ColumnID
Order By TableA.ColumnID
) AS Count_Row_No
```
这是根据ColumnID，看看同一ColumnID出现的次数。

所以本案例的做法如下：  

```sql
Select DISTINCT
StudentID
,Last_Name
,First_Name
,Gender
,GradeLevel
,Class
,Pupil_Email
,Relationship
,MIN(Pupil_Parent_Email) AS Pupil_Parent_Email
,ROW_NUMBER() OVER (
PARTITION By TableA.StudentID
Order By TableA.StudentID
) AS Count_Row_No

From TableA

Group By StudentID
,Last_Name
,First_Name
,Gender
,GradeLevel
,Class
,Pupil_Email
,Relationship
```

### Excel实现方式
实际上，Excel可以通过非常简单的方法实现计数。  
`=COUNTIF($E$2:$E2,E2)`


## Step 4 PIVOT
最后，我们需要将邮箱从列变成行

```sql
Select * From 
(
Select DISTINCT
StudentID
,Last_Name
,First_Name
,Gender
,GradeLevel
,Class
,Pupil_Email
/**
我们需要将关系，从表中隐藏，这样才能在PIVOT中将行变成列
**/
--,Relationship
,MIN(Pupil_Parent_Email) AS Pupil_Parent_Email
,ROW_NUMBER() OVER (
PARTITION By TableA.StudentID
Order By TableA.StudentID
) AS RelationEmailCount

From TableA

Group By StudentID
,Last_Name
,First_Name
,Gender
,GradeLevel
,Class
,Pupil_Email
,Relationship
) As BaseTable
PIVOT (
	MAX(Pupil_Parent_Email)
	FOR [RelationEmailCount] in ([1],[2])
) As Result
Order By Last_Name
```
结果如下：  

| StudentID | Last_Name |	First_Name |	Gender |	GradeLevel |	Class |	Pupil_Email |	1 |	 2 |
|5014|	Liu|	Aileen 	| F 	| Grade 2  Bilingual |	BG2 D	| 5014@example.com |	ccc@tt.com |	ddd@gg.com |
|5013|	Wang|	Zack	|M|	Grade 9 Senior	|SG9 B |	5013@example.com |	aaa@qq.com |	bbb@qq.com|
|5029|	Yan|	Yuki|	M|	Grade 3 Bilingual	|BG3 H	 | 5029@example.com |	f@f.com	| 2@g.com|
|5017|	Ying|	Eason|	F	|Grade 9 Senior|	SG9 A | 5017@example.com |	e@e.com |	NULL|