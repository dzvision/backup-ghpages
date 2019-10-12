---
layout: post
title: 如何利用Python杀进程并保持驻留后台检测
categories: Python
description: 
keywords: Python, Windows
---

## 如何利用Python杀进程并保持后台检测驻留

**目录**

* TOC
{:toc}

## 序
因为有一些软件一直驻留，想删的话之后又重新出现了，所以想到利用Python来进行杀进程。  

## 安装Python和使用PyChram编译器
Python的安装在这里并不想多少，目前网络上的教程都是正确的。
自从用了PyChram的编译器，世界更加美好了。编译环境可以根据每个项目不一样而不同。
下载地址：https://www.jetbrains.com/pycharm/



## 安装psutil库
psutil默认是没有这个库的，文档可以参考[psutil wiki](https://psutil.readthedocs.io/en/latest/)  

命令安装
```
pip install psutil
```

## 群发命令
```python
import os, psutil
from time import sleep
p = psutil.Process()
active = 1
while active == 1 :
    if p.name() == 'OUTLOOK.EXE':
        os.system('taskkill /IM OUTLOOK.EXE /F')
        sleep(20)
    else:
        sleep(60)
    active = 0

while active == 0 :
    if p.name() == 'OUTLOOK.EXE':
        os.system('taskkill /IM OUTLOOK.EXE /F')
        active = 1
        sleep(20)
    else:
        active = 0
        sleep(60)

```
使用while是因为不用的话，进程会自己结束，然后就没有然后了。  
所以使用了无限循环来驻留这个程序。  

最简洁的命令其实是  
```python
os.system('taskkill /IM OUTLOOK.EXE /F')
```