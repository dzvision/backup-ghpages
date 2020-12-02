---
layout: post
title: Excel中如何批量重命名工作表与将每个工作表导出到单独Excel文件
categories: Excel
description: Excel中如何批量重命名工作表与将每个工作表导出到单独Excel文件
keywords: Excel, vba, python
---




**目录**

* TOC
{:toc}

## Excel中通过VBA批量重命名工作表Worksheet
[Microsoft Docs](https://docs.microsoft.com/en-us/office/troubleshoot/excel/use-macro-rename-sheet)

Step 1: 打开Developer Tab找到VBA (快捷键 Alt+F11)  

Step 2:  Insert -->Module

Step 3:  

将以下代码复制进去
```
Sub RenameSheet()

Dim rs As Worksheet

For Each rs In Sheets
rs.Name = rs.Range("B5")
Next rs

End Sub
```

Step 4: 按F5运行，或关闭VBA后，通过 Excel View -->Macros -->View Macros-->Run


## Excel中通过VBA批量修改特定位置颜色
### 单个无条件修改全部工作表
```
Sub BackGroudColor()

Dim rs2 As Worksheet

For Each rs2 In Sheets
rs2.Range("C6").Interior.Color = RGB(180, 198, 231)
rs2.Range("B7").Interior.Color = RGB(255, 230, 153)
rs2.Range("E6").Interior.Color = RGB(198, 224, 180)
Next rs2

End Sub
```  

### 有条件修改目前工作表
```
Sub Fill_Cell_Condition()

Dim rngCell As Range
    
For Each rngCell In Range("A6:A19")
	If Len(rngCell.Value) <> "0" Then
		rngCell.Cells.Interior.Color = RGB(255, 230, 153)
	'If Everything in A6-A19 The length of the cell value is not zero, change backgroud color. Otherwise, do nothing
 End If
Next rngCell
```



## 将每个工作表导出到单独Excel文件 

Step 1: 在Termianl选择pip install组件
```
pip install pypiwin32
```


Step 2: 使用pycharm并填写代码
```python
# This is a sample Python script.

# Press Shift+F10 to execute it or replace it with your code.
# Press Double Shift to search everywhere for classes, files, tool windows, actions, and settings.
def create_wb_from_ws():
    try:
        filepath = 'D:\sp\test.xlsx'

        from win32com.client import DispatchEx
        excel = DispatchEx("Excel.Application")

        if excel == None:
            print('-' * 100)
            print('Error: Excel is not found on this machine. Existing!')
            print('-' * 100)
            return
        else:
            print('-' * 100)
            print('Message: Excel version {0} is available.'.format(excel.version))
            print('-' * 100)

        if int(float(excel.version)) < 12:
            fileext = '.xls'
        else:
            fileext = '.xlsx'

        import os
        if not os.path.exists(filepath):
            print('The entered file path does not exists. Existing!')
            return

        filedir = os.path.join(os.path.dirname(filepath), os.path.splitext(os.path.basename(filepath))[0])
        if not os.path.exists(filedir):
            os.mkdir(filedir)

        excel.Visible = False
        excel.DisplayAlerts = False
        wb = excel.Workbooks.Open(Filename=filepath)
        wb.Application.Visible = False

        for sheet in wb.Worksheets:
            filename = os.path.join(filedir, sheet.name + fileext)
            wbnew = excel.Workbooks.Add()
            wbnew.Application.Visible = False
            sheet.Copy(Before=wbnew.Worksheets(1))

            for s in wbnew.Worksheets:
                if s.name != sheet.name:
                    wbnew.Worksheets(s.name).Delete()

            wbnew.SaveAs(filename)
            print('Saved sheet name "{0}" as a new excel file at {1}'.format(sheet.name, filename))
            wbnew.Close(SaveChanges=1)

        wb.Close(True)
        excel.Quit()
    except:
        print('-' * 100)
        print('Error occurred')
        print('-' * 100)
        raise


if __name__ == "__main__":
    create_wb_from_ws()

```  
 

