---
layout: post
title: Android安卓系统使用fastboot无法刷入TWRP Recovery
categories: Android
description: 
keywords: Android
---

## Android安卓系统使用fastboot无法刷入TWRP Recovery

**目录**

* TOC
{:toc}

## 例子
尝试使用
```
fastboot flash recovery rec.img
#####
fastboot boot rec.img
```
都会提示错误，导致无法刷入TWRP

```
FAILED (Write to device failed in SendBuffer() (Unknown error))
```

## 原因
目前电脑都是USB 3.0+接口，只需要购买USB Hub转换为USB 2.0即可解决。


