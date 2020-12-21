---
layout: post
title: Windows10添加自定义右键菜单VS Code
categories: Windows
description: 
keywords: Windows
---

Windows10如何添加自定义右键菜单呢？例如我想把VS Code放到右键菜单，实现右键单文件，可以使用vscode打开，右键文件夹，可以使用vscode打开，右键北京空白处，可以使用vscode打开。

**目录**

* TOC
{:toc}


## Step 1 新建空白文件vscode.reg
在里面粘贴
```
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\*\shell\VSCode]
@="Open with Code"
"Icon"="D:\\Program\\Microsoft VS Code\\Code.exe"

[HKEY_CLASSES_ROOT\*\shell\VSCode\command]
@="\"D:\\Program\\Microsoft VS Code\\Code.exe\" \"%1\""


[HKEY_CLASSES_ROOT\Directory\shell\VSCode]
@="Open with Code"
"Icon"="D:\\Program\\Microsoft VS Code\\Code.exe"

[HKEY_CLASSES_ROOT\Directory\shell\VSCode\command]
@="\"D:\\Program\\Microsoft VS Code\\Code.exe" \"%V\""


[HKEY_CLASSES_ROOT\Directory\Background\shell\VSCode]
@="Open with Code"
"Icon"="D:\\Program\\Microsoft VS Code\\Code.exe"

[HKEY_CLASSES_ROOT\Directory\Background\shell\VSCode\command]
@="\"D:\\Program\\Microsoft VS Code\\Code.exe\" \"%V\""
```  
[参考链接1：](https://blog.csdn.net/GreekMrzzJ/article/details/82194913) 

## Step 2 替换文件位置
确认你的文件位置，并修改。
D:\A\B\C.exe要变成D:\\A\\B\\C.exe



## Step 3 保存并双击打开
如题

## 题外话
如果修改其他程序也是一样的，不过除了要记得修改程序的路径之外，别忘了修改注册表的路径名称。
例如我们添加Sublime Text 3, 也可以把菜单名字稍微变化一下方便识别。

```
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\*\shell\SublimeText3]
@="Edit with Sublime Text 3"
"Icon"="D:\\Program\\Sublime Text 3\\sublime_text.exe"

[HKEY_CLASSES_ROOT\*\shell\SublimeText3\command]
@="\"D:\\Program\\Sublime Text 3\\sublime_text.exe\" \"%1\""

[HKEY_CLASSES_ROOT\Directory\shell\SublimeText3]
@="Edit with Sublime Text 3"
"Icon"="D:\\Program\\Sublime Text 3\\sublime_text.exe"

[HKEY_CLASSES_ROOT\Directory\shell\SublimeText3\command]
@="\"D:\\Program\\Sublime Text 3\\sublime_text.exe" \"%V\""

[HKEY_CLASSES_ROOT\Directory\Background\shell\SublimeText3]
@="Edit with Sublime Text 3"
"Icon"="D:\\Program\\Sublime Text 3\\sublime_text.exe"

[HKEY_CLASSES_ROOT\Directory\Background\shell\SublimeText3\command]
@="\"D:\\Program\\Sublime Text 3\\sublime_text.exe\" \"%V\""
```