---
layout: post
title: Word文件内嵌入多个PPT/WORD等文件在苹果系统无法打开
categories: Office
description: Word文件内嵌入多个PPT/WORD等文件在苹果系统无法打开
keywords: Office
---



我们遇到了一个Word文件内嵌入了PPT在苹果电脑无法打开,提示错误“
the program used to create this object is powerpoint that program is not installed on your computer”


**目录**

* TOC
{:toc}

## 微软答复
[Answer](https://answers.microsoft.com/en-us/mac/forum/macoffice2016-macpowerpoint/problem-embedding-a-powerpoint-object-in-a-word/3831445c-5bf3-4af0-aa99-2530748e7753?auth=1)
微软的意思是好像macOS上不支持这类型嵌入，那么如果文件比较多，我们如何将嵌入文件在Windows电脑提取出来呢？



## 通过VBA实现提取
[datanumen](https://www.datanumen.com/blogs/2-quick-ways-extract-ms-office-files-embedded-word-document/)
  
1. First and foremost, click on “Developer” tab and then the “Visual Basic”. Or just press “Alt+ F11” instead if the “Developer” tab isn’t available.Click "Developer"->Click "Visual Basic"
2. Next click “Normal” project.
3. Then click “Insert” tab.
4. Choose “Module” on the drop-down menu.Click "Normal"->Click "Insert"->Click "Module"
5. Now double click on the new module to have the coding space.
6. And paste the bellowing codes there:

```
Sub ExtractAndSaveEmbeddedFiles()
  Dim objEmbeddedShape As InlineShape
  Dim strShapeType As String, strEmbeddedDocName As String
  Dim objEmbeddedDoc As Object
 
  With ActiveDocument
  For Each objEmbeddedShape In .InlineShapes
 
  '  Find and open the embedded doc.
  strShapeType = objEmbeddedShape.OLEFormat.ClassType
  objEmbeddedShape.OLEFormat.Open
 
  '  Initialization
  Set objEmbeddedDoc = objEmbeddedShape.OLEFormat.Object
 
  '  Save embedded files with names as same as those of icon label. 
  strEmbeddedDocName = objEmbeddedShape.OLEFormat.IconLabel
  objEmbeddedDoc.SaveAs "C:\Users\Public\Documents\New folder\" & strEmbeddedDocName
  objEmbeddedDoc.Close
 
  Set objEmbeddedDoc = Nothing
 
  Next objEmbeddedShape
  End With
End Sub
```  

7. Finally, click “Run” button or hit “F5”.Paste Codes->Click "Run"
All embedded files will be stored under a specific directory with their original names
  
### Note: 修改代码内文件储存位置
In code line “objEmbeddedDoc.SaveAs “C:\Users\Public\Documents\New folder\” & strEmbeddedDocName”, the “C:\Users\Public\Documents\New folder\” is the location for storing files. Remember to replace it with an actual one.