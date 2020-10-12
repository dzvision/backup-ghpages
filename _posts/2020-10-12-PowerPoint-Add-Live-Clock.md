---
layout: post
title: PowerPoint中如何设置现在时间并实时更新
categories: PowerPoint
description: PowerPoint VBA
keywords: PowerPoint
---

在工作中，PowerPoint做实时时间可以通过Add-in也可以通过VB来做，下面我用VB来做


**目录**

* TOC
{:toc}

## PowerPoint 设置

Step 1: 新建文本框并在文本框输入"--:--:--"

Step 2: 在Home里面找到Find下面的Select并选择Selection Pane  
![Step2](/blog/images/posts/2020/20201012_AddLiveClock-step2-SelectionPane.png)   
  
Step 3: 在右方Selection选择双击Textbox的名字并更名为ShpClock
![Step3](/blog/images/posts/2020/20201012_AddLiveClock-step3.png)   
  
Step 4: 去Options添加Developer Tab。
![Step4](/blog/images/posts/2020/20201012_AddLiveClock-step4.png)  
  
## Visual Basic设置
Step 5: 点击developer Tab然后点击Visual Basic设置  
![Step5](/blog/images/posts/2020/20201012_AddLiveClock-step5.png)  
  
Step 6: 在Microsoft Visual Basic for Applcations打开后点击Insert-->Module  
  
Step 7: 在输入代码页面输入如下代码
```
Public clock As Boolean
Public currenttime, currentday As String


Sub Pause()
Dim PauseTime, start
PauseTime = 1
start = Timer
Do While Timer < start + PauseTime
DoEvents
Loop
End Sub

Sub StartClock()
clock = True
Do Until clock = False
On Error Resume Next
currenttime = Format((Now()), "hh:mm:ss")
currenttime = Mid(currenttime, 1, Len(currenttime) - 0)
ActivePresentation.Slides(SlideShowWindows(1).View.CurrentShowPosition).Shapes("shpClock").TextFrame.TextRange.Text = currenttime
Pause
Loop
End Sub

Sub OnSlideShowPageChange(ByVal objWindow As SlideShowWindow)
clock = False
ActivePresentation.Slides(SlideShowWindows(1).View.CurrentShowPosition).Shapes("shpClock").TextFrame.TextRange.Text = "--:--:--"
End Sub

Sub OnSlideShowTerminate()
clock = False
End Sub
```
