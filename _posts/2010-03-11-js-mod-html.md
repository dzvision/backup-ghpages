---
layout: post
title: JS 修改网页大法 - 一段代码，编辑整个网页~
categories: HTML
description: HTML
keywords: HTML
---

在浏览器地址栏输入这一行代码，然后回车，就发现整个页面都可以随意编辑了。仅仅是一行很短的代码。
```
javascript:document.body.contentEditable='true'; document.designMode='on';!msn1dai
```
疏影试过了，很有效  

或：
```
javascript: document.body.contentEditable = 'true';﻿document.designMode = 'on'; void 0
```