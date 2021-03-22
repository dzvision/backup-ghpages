---
layout: post
title: Excel中如何设置随机密码
categories: Excel
description: Excel中如何设置随机密码
keywords: Excel
---




**目录**

* TOC
{:toc}

## Excel中设置随机数字
[Lifewire](https://www.lifewire.com/use-rand-function-to-create-random-numbers-in-excel-4178642#:~:text=1%20Click%20on%20a%20worksheet%20cell%20where%20you,Now,%20pressing%20F9%20won't%20affect%20the%20random%20number.)

Step 1: 

将以下代码复制进去
```
=TRUNC(RAND()*(High-Low)+Low)
##
=TRUNC(RAND()*(3000-1000)+1000)
## 或者：
=RANDBETWEEN(1000,3000)
```



## Excel中设置随机字母
[ExcelZoom](https://excelzoom.com/generate-a-random-character-string/#:~:text=To%20generate%20a%20random%20number%20string%20in%20Excel%2C,page%20is%20refreshed.%20Generate%20Random%20Uppercase%20Letter%20String)


```
#大写字母
=CHAR(RANDBETWEEN(65,90))

#小写字母
=CHAR(RANDBETWEEN(97,122))

#特殊字符
=CHAR(RANDBETWEEN(33,47))
```  

#合并成密码

```
=CHAR(RANDBETWEEN(65,90))&CHAR(RANDBETWEEN(97,122))&CHAR(RANDBETWEEN(97,122))&CHAR(RANDBETWEEN(97,122))&RANDBETWEEN(1000,3000)
```  

最后通过复制该列并粘贴成值即可。
 

