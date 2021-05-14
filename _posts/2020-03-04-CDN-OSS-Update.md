---
layout: post
title: 如何给网站添加CDN和OSS呢?
categories: HTML
description: 
keywords: HTML
---


**目录**

* TOC
{:toc}

## 序
由于我自己的个人网站是放在韩国首尔的甲骨文云上，在中国部分地区确实无法快速访问。
于是我想通过CDN+OSS的方式来加速访问。

## 1. 调研CDN
经过调研后，小牌子的CDN跟没有用没有什么区别，而大牌子的CDN要你的域名经过ICP备案才可以。
本来看了七牛云和又拍云，他们都有免费CDN+OSS的方式。七牛云不支持HTTPS, 而又拍云支持。
又拍云只要你申请联盟，就可以获得。  
https://www.upyun.com/league

## 2. 改用jsDelivr
CDN+OSS方案因为备案无法通过，所以暂时被搁置了。  
jsDelivr CDN是和国内大品牌合作的免费CDN, 所以静态的文件加速，我最后选择了他。


## 3. jsDelivr CDN + GitHub
使用jsDelivr，就要上传文件到GitHub仓库里面，新建一个仓库并上传完文件之后，点击Release。  
版本号填写1.0 然后发布即可。

## 4. jsDelivr CDN的使用方式
例子：
https://cdn.jsdelivr.net/gh/你的GitHub用户名/你的仓库名@版本号/assets/demo.css  
如果你的版本号是1.0那么就是1.0，是v1.0那么就是填写v1.0  
版本号后面就是资源的github这个仓库下面的具体地址  
https://cdn.jsdelivr.net/gh/exampleusername/examplerepo@1.0/assets/demo.css  

你也可以不填写版本号来实现，但是可能会出现问题。

## 5. OSS选用
静态网页加速可以这样解决，那么如果我有视频，或者音频呢？放GitHub不太好。
在这里，我选择了京东云OSS, 免费10GB的储存，并且很方便就直接用上了外链，这跟网盘的操作方式是一样的。

## 6. 图床白嫖
图床我以前是使用百度贴吧，通过发帖发布图片得到地址而免费白嫖的。不过目前最新方法是可以通过API的方式白嫖各大厂的图床。
例子：<https://github.com/BlueSkyXN/KIENG-FigureBed>

