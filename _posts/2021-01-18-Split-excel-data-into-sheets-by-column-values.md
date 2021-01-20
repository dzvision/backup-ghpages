---
layout: post
title: 如何根据Excel某列数据为依据分成一个新的工作表
categories: excel
description: 
keywords: python, excel
---

我们有时候需要将表单内的某列数据分到新的工作表里。

**目录**

* TOC
{:toc}


## 示例表

| StudentID | Last_Name | First_Name | Gender | GradeLevel | Class | Pupil_Email	| Relationship |	Pupil_Parent_Email |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| 5013 |	Wang |	Zack | M |	Grade 9 Senior |	SG9 B |	5013@example.com |	爸爸 |	5013a@qq.com |
| 5013 |	Wang |	Zack |	M |	Grade 9 Senior |	SG9 B |	5013@example.com |	妈妈 |	5013b@qq.com |
| 5014 |	Liu |	Aileen |	F |	Grade 2 Bilingual	 | BG2 D | 	5014@example.com |	爸爸	 | 5014a@qq.com |
| 5014 |	Liu |	Aileen |	F |	Grade 2 Bilingual	 | BG2 D | 	5014@example.com | 妈妈 | 5014b@qq.com |
| 5014 |	Liu |	Aileen |	F |	Grade 2 Bilingual	 | BG2 D | 	5014@example.com | 妈妈 | 5014b@qq.com |
| 5017 |	Ying | 	Eason | 	F | 	Grade 9 Senior | 	SG9 A |	5017@example.com |	爸爸	| 5017e@qq.com | 
| 5017 |	Ying | 	Eason | 	F | 	Grade 9 Senior | 	SG9 A |	5017@example.com |	爸爸	| 5017e@qq.com | 
| 5029	| Yan	| Yuki	| M	| Grade 3 Bilingual	| BG3 H	| 5029@example.com	| 爸爸	| 5029a@qq.com | 
| 5029	| Yan	| Yuki	| M	| Grade 3 Bilingual	| BG3 H	| 5029@example.com	| 妈妈 | 5029b1@qq.com | 
| 5029	| Yan	| Yuki	| M	| Grade 3 Bilingual	| BG3 H	| 5029@example.com	| 妈妈 | 5029b2@qq.com |
| 5029	| Yan	| Yuki	| M	| Grade 3 Bilingual	| BG3 H	| 5029@example.com	| 妈妈 | 5029b3@qq.com |

## 解析
首先我们先按年级将表格分为新的文件。之后我们将按照班级分工作表


## Step 1 Separate Excel Data into Workbooks by Column Values Using Python
[1. Youtube](https://www.youtube.com/watch?v=ZlxgW_65GF8)    
[2. GitHub](https://github.com/Derrick-Sherrill/DerrickSherrill.com/blob/master/separate_by_value.py)  

首先需要pip3 install pandas和pip3 install openpyxl


```python
import pandas as pd

excel_file_path = 'training_status.xlsx'
# Windows文件路径记得要多一个斜杠 D:\\Projects\\
# 或者用反斜杠

df = pd.read_excel(excel_file_path)
# print(df)

split_values = df['Shift'].unique()
# print(split_values)

for value in split_values:
    df1 = df[df['Shift'] == value]
    output_file_name = "Shift_" + str(value) + "_Trainings.xlsx"
    df1.to_excel(output_file_name, index=False)
```



## Step 2 Separate Excel Data into new sheets by Column Values - VBA
虽然Python也可以做，但是我实践没实践出来。  
[stackoverflow](https://stackoverflow.com/questions/49408744/split-dataframe-according-to-column-value-and-export-to-different-excel-workshee)  
[Kudo Tools](https://www.extendoffice.com/documents/excel/1174-excel-split-data-into-multiple-worksheets-based-on-column.html)

1. Hold down the ALT + F11 keys to open the Microsoft Visual Basic for Applications window.  
2. Click Insert > Module, and paste the following code in the Module Window.  
3. 关闭VBA窗口，在Excel表Tab中的Developer中点击Macros。  
4. 在弹出Macro窗口选择Splitdatabycol并点击Run即可。
5. 然后代码运行之后，会弹出第一个窗口，选择全部表头（标题）{$A$1:$D$1}
6. 第二个弹出框选择，除去标题的全部列。{$B$2:$B$17}

```
Sub Splitdatabycol()
'updateby Extendoffice
Dim lr As Long
Dim ws As Worksheet
Dim vcol, i As Integer
Dim icol As Long
Dim myarr As Variant
Dim title As String
Dim titlerow As Integer
Dim xTRg As Range
Dim xVRg As Range
Dim xWSTRg As Worksheet
On Error Resume Next
Set xTRg = Application.InputBox("Please select the header rows:", "Kutools for Excel", "", Type:=8)
If TypeName(xTRg) = "Nothing" Then Exit Sub
Set xVRg = Application.InputBox("Please select the column you want to split data based on:", "Kutools for Excel", "", Type:=8)
If TypeName(xVRg) = "Nothing" Then Exit Sub
vcol = xVRg.Column
Set ws = xTRg.Worksheet
lr = ws.Cells(ws.Rows.Count, vcol).End(xlUp).Row
title = xTRg.AddressLocal
titlerow = xTRg.Cells(1).Row
icol = ws.Columns.Count
ws.Cells(1, icol) = "Unique"
Application.DisplayAlerts = False
If Not Evaluate("=ISREF('xTRgWs_Sheet!A1')") Then
Sheets.Add(after:=Worksheets(Worksheets.Count)).Name = "xTRgWs_Sheet"
Else
Sheets("xTRgWs_Sheet").Delete
Sheets.Add(after:=Worksheets(Worksheets.Count)).Name = "xTRgWs_Sheet"
End If
Set xWSTRg = Sheets("xTRgWs_Sheet")
xTRg.Copy
xWSTRg.Paste Destination:=xWSTRg.Range("A1")
ws.Activate
For i = (titlerow + xTRg.Rows.Count) To lr
On Error Resume Next
If ws.Cells(i, vcol) <> "" And Application.WorksheetFunction.Match(ws.Cells(i, vcol), ws.Columns(icol), 0) = 0 Then
ws.Cells(ws.Rows.Count, icol).End(xlUp).Offset(1) = ws.Cells(i, vcol)
End If
Next
myarr = Application.WorksheetFunction.Transpose(ws.Columns(icol).SpecialCells(xlCellTypeConstants))
ws.Columns(icol).Clear
For i = 2 To UBound(myarr)
ws.Range(title).AutoFilter field:=vcol, Criteria1:=myarr(i) & ""
If Not Evaluate("=ISREF('" & myarr(i) & "'!A1)") Then
Sheets.Add(after:=Worksheets(Worksheets.Count)).Name = myarr(i) & ""
Else
Sheets(myarr(i) & "").Move after:=Worksheets(Worksheets.Count)
End If
xWSTRg.Range(title).Copy
Sheets(myarr(i) & "").Paste Destination:=Sheets(myarr(i) & "").Range("A1")
ws.Range("A" & (titlerow + xTRg.Rows.Count) & ":A" & lr).EntireRow.Copy Sheets(myarr(i) & "").Range("A" & (titlerow + xTRg.Rows.Count))
Sheets(myarr(i) & "").Columns.AutoFit
Next
xWSTRg.Delete
ws.AutoFilterMode = False
ws.Activate
Application.DisplayAlerts = True
End Sub
```
