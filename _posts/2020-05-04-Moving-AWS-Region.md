---
layout: post
title: AWS EC2实例迁移教程
categories: 服务器
description: 搭建Windows/Office KMS服务器
keywords: 服务器, AWS
---

因为之前建立AWS EC2的时候太过着急，区域选错了。所以等了一段时间之后，迁移EC2到新加波。  
参考来源:[如沙雨下](https://www.jianshu.com/p/0d2acb2334d0)


**目录**

* TOC
{:toc}

## 1. 创建AMI

在EC2的位置点击右键 映像-->创建映像。等待创建完成。

## 2. 迁移AMI
在侧边栏里面找到"映像->AMI"，然后在AMI里面选择创建完成的AMI映像。并点击复制映像。
之后在区域里面选择你想要的区域。

## 3. AWS区域选择
选择对自己速度最好的区域。在这里我感觉新加坡的速度比较不错。（东京的好像听说完全不行，实测Ping值非常高）

### 3.1 Ping测试
从浏览器中，利用你的地址测试Ping
1. <https://www.cloudping.info/>  

2. <https://cloudharmony.com/speedtest-for-aws>

实际测试中，第一个非常直观看到AWS区域的速度，而第二个测试非常慢，不太可行。

### 3.2 IP查询与实测
我们可以从官方网站中得到区域的测试IP
<http://ec2-reachability.amazonaws.com/>  

然后利用这个IP 进行Ping和TraceRoute。  

例如我们通过以下2个网站来测试Ping / Get  

<http://ping.chinaz.com/>  

<https://www.17ce.com/>

## 4. 开启实例
迁移好对的区域之后，我们就可以准备开启实例。
直接在实例里面，选择“你的AMI”，然后找到刚刚迁移（复制）好的AMI实例。  
之后的流程就是开启实例的流程。
需要注意的是，会要求创建钥匙对，但是这个钥匙对实际上是不能用的。
我们依然使用旧的钥匙对来SSH。


## 5. 确保删除不必要的东西
确保删除好旧区域内全部东西，以及在新区域内的AMI：即取消注册之后，然后再删除EBS快照。避免不必要的费用。