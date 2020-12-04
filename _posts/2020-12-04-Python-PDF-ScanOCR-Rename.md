---
layout: post
title: 如何利用Python批量重命名PDF文件
categories: Python
description: 
keywords: Python, Windows, PDF
---

除了普通的文件名修改，我们还可以将PDF内容提取出来并用于重命名

**目录**

* TOC
{:toc}
  

## 安装Python和使用PyChram编译器
Python的安装在这里并不想多少，目前网络上的教程都是正确的。
自从用了PyChram的编译器，世界更加美好了。编译环境可以根据每个项目不一样而不同。
下载地址：https://www.jetbrains.com/pycharm/  


## 安装Jupyter Notebook
如果不安装Jupyter Notebook就无法在测试的时候显示出我们想要的效果，可能跟依赖包有关系。
在Terminal安装：  
```python
pip3 install jupyter
```

## 安装tabula

在Terminal安装：  
```python
pip install tabula-py
```

## 代码测试
运行以下代码测试：
```
import tabula

demo = tabula.read_pdf('C:\\Users\\UserName\\Downloads\\1.pdf')
df2 = tabula.read_pdf("https://github.com/tabulapdf/tabula-java/raw/master/src/test/resources/technology/tabula/arabic.pdf")
print(demo)

```
这个时候其实已经出来了，不过你也可以用Jupyter Notebook来进行测试：  
在Terminal输入
```
jupyter notebook
```
这个时候会自动在浏览器打开Jupyter

由于我自己要测试用的文档无法使用，故而废弃。

## 参考文献
[1. CSDN](https://blog.csdn.net/weixin_40796925/article/details/102867098)
[2. 知乎](https://zhuanlan.zhihu.com/p/33105153)
[3. Towards Data Science](https://towardsdatascience.com/scraping-a-table-in-a-pdf-reliably-and-then-test-data-quality-6718bb91d471)