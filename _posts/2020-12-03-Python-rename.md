---
layout: post
title: 如何利用Python批量重命名文件
categories: Python
description: 
keywords: Python, Windows
---

我们有时候遇到文件名刚好调转，需要重新命名一下。

**目录**

* TOC
{:toc}
  

## 安装Python和使用PyChram编译器
Python的安装在这里并不想多少，目前网络上的教程都是正确的。
自从用了PyChram的编译器，世界更加美好了。编译环境可以根据每个项目不一样而不同。
下载地址：https://www.jetbrains.com/pycharm/  


## 文件名前后互换
将学生名字放到前面而不是后面。
即：500215-John Doe改为John Doe-500215  
  
```python
import os
path='C:\\Users\\UserName\\Desktop\\intro'
# 文件路径格式需要注意！
# 以下是可以使用的格式
#C:\\Users\\Administrator\\Desktop\\intro\\
#C:/Users/Administrator/Desktop/intro/

#获取该目录下所有文件，存入列表中
fileList=os.listdir(path)
#定义文件前缀和后面部分列表
studentID=[]
studentName=[]

n=0
for i in fileList:
    #设置旧文件名（就是路径+文件名）
    oldname=path+os.sep+fileList[n] #os.sep添加系统分隔符
    #print(fileList[n][7:len(fileList[n])-5])
    studentID.insert(n,fileList[n][0:6])
    studentName.insert(n,fileList[n][7:len(fileList[n])-5])
    #len(fileList[n])-5 代表减去了.xlsx文件后缀名

    #设置新文件名
    newname=path+os.sep+studentName[n] + '-'+ studentID[n] + '.xlsx'
    #用os模块中的rename方法对文件改名
    os.rename(oldname,newname)
    print(oldname,'======>',newname)
    n += 1


```

## 特定字符前后对换
如果我想将姓放在前面呢？  
因为空格位置每个文件不一样，我们怎么做呢？
可不可以根据数据其中一个特定字符，得到这个字符位于单词的位置？
我们可以从下面例子得到一些灵感。  
```
ls = ["a", "b", "c", "d", "e"]
print(ls.index("c"))

>>>2
## 进阶

ls = ["apple", "banana", "coco", "delta", "echo"]
print(ls[0].index("l"))
>>>3
```

完整代码
```python
import os
path='C:\\Users\\Xadmin\\Desktop\\intro'
# 文件路径格式需要注意！
# 以下是可以使用的格式
#C:\\Users\\Administrator\\Desktop\\intro\\
#C:/Users/Administrator/Desktop/intro/

#获取该目录下所有文件，存入列表中
fileList=os.listdir(path)
#定义文件前缀和后面部分列表
firstName=[]
lastName=[]
StudentID=[]

n=0
for i in fileList:
    #设置旧文件名（就是路径+文件名）
    oldname=path+os.sep+fileList[n] #os.sep添加系统分隔符
    #print(fileList[n][0:len(fileList[n])-5])
    #print(fileList[n].index(" "))
    #len(fileList[n])-5]
    firstName.insert(n, fileList[n][0:fileList[n].index(" ")])
    lastName.insert(n, fileList[n][fileList[n].index(" ")+1:fileList[n].index("-")])
    StudentID.insert(n, fileList[n][fileList[n].index("-")+1:len(fileList[n])-5])
    # len(fileList[n])-5 代表减去了.xlsx文件后缀名
    #print(lastName[n]+' '+firstName[n] + '-'+ StudentID[n])

    #设置新文件名
    newname=path + os.sep + lastName[n]+' '+firstName[n] + '-'+ StudentID[n] + '.xlsx'
    #用os模块中的rename方法对文件改名
    os.rename(oldname,newname)
    print(oldname,'======>',newname)
    n += 1



```

