---
layout: post
title: 如何利用Python和wxpy进行群发
categories: Python
description: 
keywords: Python Wechat
---

## 如何利用Python和wxpy进行群发

**目录**

* TOC
{:toc}

## 序
使用Python进行微信网页版模拟早已不是秘密，甚至可以使用鼠标模拟的方式，对PC版进行模拟。  
[WeTool免费版](https://www.wxb.com/wetool)，能直接查看全部好友是否有人删除了你，并且不会发送信息给朋友，使用这个可能比Python更合适一些。  
另外[句子秒回](https://wechat.botorange.com/)也是一个不错的工具，他更多聚焦在CRM上面。

下面，我们一起来探究一下如何进行群发。

## 安装Python
Python的安装在这里并不想多少，目前网络上的教程都是正确的。
需要指出的是，使用Python进行群发，由于编码问题，可能建议不要使用原装编译器。  
否则在运行的时候可能出错。
好像据说安装了pystorm也可以,但是我并没有测试，我是使用PyChram来编译运行的。
下载地址：https://www.jetbrains.com/pycharm/



## 安装wxpy库
wxpy默认是没有这个库的，安装方式可以参考[GitHub](https://github.com/youfou/wxpy)

国内用户建议使用如下命令安装
```
pip install -U wxpy -i "https://pypi.doubanio.com/simple/"
```

## 群发命令
```python
from wxpy import *
from time import sleep
import random

bot = Bot(cache_path=True)
#cache_path="D:\PycharmProjects\TestProject1\wxpy.pkl"可以直接设置pkl缓存的位置
#但是你也可以直接用cache_path=True来执行

message = input('请输入要发送的微信信息：')
#此次将发送全部好友
my_friend = bot.friends()
for i in range(1, len(my_friend)):
    #从1开始代表除去自己，从0开始表示包含自己。
    loadtime = random.uniform(2, 10)
    # 防止微信账号违规操作被封，每次发送信息时间间隔为随机2-10s'
    sleep(loadtime)
    print(loadtime)
    my_friend[i].send(message)#发送信息
print('已完成')
```

## 其他有趣的命令
男女比例查询  
```python
from wxpy import *
def get_friend_sex(friends):
    male = female = other = 0
    for i in friends[1:]:
        sex = i.sex
        if sex == 1:
            male += 1
        elif sex == 2:
            female += 1
        else:
            other += 1
    return male, female, other

bot = Bot(cache_path=True)
bot.file_helper.send('hello world!')
friends = bot.friends()

male, female, other = get_friend_sex(friends)
total = len(friends[1:])
# 好了，打印结果
print("男性好友：%.2f%%" % (float(male) / total * 100))
print("女性好友：%.2f%%" % (float(female) / total * 100))
print("其他：%.2f%%" % (float(other) / total * 100))
```
