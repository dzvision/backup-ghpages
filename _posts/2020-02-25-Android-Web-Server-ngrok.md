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

## 1. 安装Apache HTTP Server
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

