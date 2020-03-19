---
layout: post
title: 如何做一个Email模板HTML并导入进邮箱内
categories: MacOS
description: 
keywords: MacOS
---


**目录**

* TOC
{:toc}

## 序
使用Mailchimp.com用于制作模板

## 1. 
制作好Campaigns，记得点击Edit Design, 然后在右上角Template点击Save this Design as templates.  
然后在Brand --> Templates点击Export as HTML  

## 2. 更换图片源
使用Mailchimp的图片库，会导致中国大陆无法访问图片。也正是因为如此，才需要下载HTML来做进一步修改。  
在我的例子里将mcusercontent.com的图片地址全部修改为我的域名放置图片地址。
```
<img align="center" alt="" src="https://example.com/1.jpg" width="564" style="max-width:600px; padding-bottom: 0; display: inline !important; vertical-align: bottom;" class="mcnImage">
```

但是，单独修改图片源地址，图片的大小格式不知为何会在嵌入Outlook的时候不按比例来。所以我额外添加了height参数
```
<img align="center" alt="" src="https://example.com/2.jpg" width="600" height="360" style="max-width:600px; padding-bottom: 0; display: inline !important; vertical-align: bottom;" class="mcnImage">
```
对于图标等影响不大的，可以直接用width="50%"的方式设置。    

## 3. 在新版本Outlook中添加老版本Attach File
[参考链接1](https://www.msoutlook.info/question/insert-html-code-directly-into-an-email)
[参考链接2](https://www.msoutlook.info/question/classic-attach-file-button)

通过Options-->Quick Access Toolbar 然后选择All Commands,找到Attach File(不是Attach File...)
然后添加进去。  


## 4. 使用Outlook 老版本Attach File嵌入HTML
点击左上角快捷工具的Attach File,并选择好HTML。之后，选择Insert as Text.

## 5. 查看效果
查看Outlook 发送效果以及网页端效果。


