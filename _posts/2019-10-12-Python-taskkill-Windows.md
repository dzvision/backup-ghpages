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

## 杀死进程
```python
import psutil
from time import sleep
active = 1 #并无意义的flag 正好可以做一个while无限循环
process_to_kill = 'QQBrowser.exe'
while active == 1 :
    for proc in psutil.process_iter():
        #进程名字清单
        try:
            if proc.name().lower() == process_to_kill.lower(): #进程名字对比（变成小写对比）
                print(proc.pid) #proc.pid就是该进程PID
                p = psutil.Process(proc.pid)
                #定义P为这些进程PID
                p.terminate()
                #通过这个内置功能杀进程的方式直接删除这些进程
                #你也可以通过os.system('taskkill /IM QQBrowser.exe /F')
                #的方式删除,需要import os
                print('Successfully kill', process_to_kill, 'apps.')
        except psutil.NoSuchProcess:
            pass
    sleep(15)
```
使用while是因为不用的话，进程会自己结束，然后就没有然后了。  
所以使用了无限循环来驻留这个程序。  

最简洁的命令其实是  
```python
import os

os.system('taskkill /IM OUTLOOK.EXE /F')
```

## 杀死进程高阶版 - 杀死多进程
实际上，使用pid和terminate并不是特别高效
我们还可以使用kill来实现  
```python
import psutil
from time import sleep
active = 1 #并无意义的flag 正好可以做一个while无限循环
process_to_kill = {'QQBrowser.exe', 'QQMusic.exe', 'QQImage.exe'}
#List里面无法直接变成小写，具体可以Google
while active == 1 :
    for proc in psutil.process_iter():
        #进程名字清单
        try:
            if proc.name() in process_to_kill:
                proc.kill()
                print('Successfully kill those apps.')
        except psutil.NoSuchProcess:
            pass
    sleep(15)
```

## 杀死进程60秒后自动结束版
如果是无限循环的话，让进程一直存在似乎不太好，于是就想到自动结束进程的方法。   
来源：[stackoverflow](https://stackoverflow.com/questions/20775624/end-python-code-after-60-seconds)
```python
import os
import time
import psutil
from datetime import datetime
from threading import Timer



def exitfunc():
    print("Exit Time", datetime.now())
    os._exit(0)

Timer(60, exitfunc).start() # exit in 60 seconds

while True: # infinite loop, replace it with your code that you want to interrupt
    print("Current Time", datetime.now())
    time.sleep(1)
    process_to_kill = {'AdobeARM.exe', 'acrotray.exe','QQProtect.exe','pcas.exe','wwbizsrv.exe','dy_service.exe'}
    #List里面无法直接变成小写，具体可以Google
    for proc in psutil.process_iter():
          #进程名字清单
        try:
            if proc.name() in process_to_kill:
                proc.kill()
                print('Successfully kill those apps.')
        except psutil.NoSuchProcess:
            pass
```			