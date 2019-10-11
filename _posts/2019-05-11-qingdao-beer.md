---
layout: post
title: 青岛啤酒联通每天领流量90M
categories: Python
description: 每天领流量
keywords: 中国联通, Python
---

青岛啤酒活动，联通每天领3次共90M流量
网页挂了，用python继续领！

**目录**

* TOC
{:toc}

## 1. 下载python 3.7并安装

### 下载python 3.7
python官网：https://www.python.org/downloads/release/python-373/


### 安装python



## 2. 新建xxx.py

```
import requests as r
import time
 
def f1(num):
    data1 = {
        'phoneVal': num,
        'type': '21'
        }
    #获取验证码
    print(r.post('https://m.10010.com/god/AirCheckMessage/sendCaptcha', data = data1).text)
      
    #领取流量
    print(r.get('https://m.10010.com/god/qingPiCard/flowExchange?number=%s&type=21&captcha=%s' % (num, input('验证码: ').strip())).text)
   
phonenumber=input("请输入手机号：")
  
for i in range(3):
    print('==第{}次领取=='.format(i+1))
    f1(phonenumber)
    if i==2:
        print('今天已经领完啦！请明天再来吧。')
        print('程序将在5s后退出。。。')
        time.sleep(65)
    else:
        print('请等待65s后面还有{}次哦'.format(2-i))
        time.sleep(65)
```



## 3. 安装requests
因为python默认是没有request库，所以我们需要cd到python目录然后安装。
否则的话，在运行的时候会出错。

```
##转到python安装目录
cd C:\Users\David\AppData\Local\Programs\Python\Python37  

##安装缺少的库
pip install requests

```

## 4. 用IDLE打开xxx.py
使右键点击xxx.py, 使用idle编辑器打开 
然后点击Run--> Run Module即可

