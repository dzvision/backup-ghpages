---
layout: post
title: 使用Android手机实现Web服务器 - 内网穿透
categories: 网页服务器
description: 
keywords: 网页服务器
---


**目录**

* TOC
{:toc}

## 序
使用Android手机实现Web服务器，其中包含如何安装Apache HTTP Server以及如何使用Ngrok(Sunny)的服务反向代理。

##  方法一的尝试：1. 安装Apache HTTP Server
安装Apache HTTP Server前，需要先安装Termux
先从Google Play下载。


### 1.1 安装Apache前准备
打开Termux后，
输入
```
apt update
```
确保手机更新好源。  

然后输入
```
apt install apache2
```
之后再询问中回答y即可安装。

### 1.2 安装完成后
安装好之后
Termux的命令行会变成$, 如下
```
Setting up apache2 (2.4.41-3) ...
$
```  

这个时候你只在$后需要输入apachectl
```
$ apachectl
```
即可运行apache

需要注意的是，他会弹出
```
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using l127.0.0.1. 
Set the 'ServerName' directive globally to suppress this message
```
这个问题暂时不用理他

### 1.3 浏览手机浏览器或通过电脑浏览
手机通过127.0.0.1:8080访问  
电脑通过路由器中手机的IP地址访问  
例如192.168.2.200:8080  
只要出现It Works即可证明网页服务器工作。


### 1.4 网页服务器位置
输入
```
$ cd ..
$ ls
```
之后会出现蓝色字体  
```
home usr
```
然后输入
```
$ cd usr/share/apache2
$ ls
```
可以从这里看出蓝色字体的文件夹是  
default-site
而这个文件夹下面，也还有一个文件夹是叫htdocs  
进入到htdocs文件夹之后，即可发现index.html  

实际完整地址
```
/data/data/com.termux/files/usr/share/apache2/default-site/htdocs/
```
另外需要注意的是当Termux被关闭后，apachectl也会被关闭。

### 把Apache默认网页位置修改到SD卡
暂无解决方案

## 代替方案KSWEB和谐版

### KSWEB和谐版下载地址


### ngrok sunny内网穿透
注册sunny的ngrok并生成clientid.
然后下载sunny的ngrok的python版本
通过
```
pkg install python
```
安装
具体安装步骤可以查看
http://www.ngrok.cc/_book/start/ngrok_android.html  

但是我后来发现需要root才可以运行python
于是在termux里面运行apt install tsu
通过tsu命令得到root
最后我发现，由于这个免费服务器是海外的，IP被封了。  
用不了。（测试，打开VPN后可以用，但是这等于没用。）

## 方法二 花生壳实现内网穿透
因为ngrok内网穿透方案看过之后，类似的内网穿透方案例如frp,lanproxy等原理都相似。  
都需要一台VPS运转，且若包含了免费VPS给你用的话，也是在海外，一样有带宽限制。  

如果有VPS的话， 这个配置我还不如直接vps装面板，还能支持多个网站。  
  
所以，回归到花生壳也是必须只能这样。花生壳的免费服务器是上海的，不会担心IP封。 

花生壳改变了很多，无法进行域名解析了，只能先用电脑端打开花生壳超过1个小时，耐心等待花生壳的DNS自动修改IP为新的IP。
设置好各个端口之后，去DNS服务商设置CNAME为你的花生壳二级域名即可。  
  
需要注意的是，如果你采用了企业邮箱，你的CNAME就无法直接用@的形式，必须是www  
不过，你也可以增加A解析到你CNAME的IP地址。  





