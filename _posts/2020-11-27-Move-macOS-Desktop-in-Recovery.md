---
layout: post
title: macOS在恢复模式中移动Desktop内文件到Documents内
categories: macOS
description: 
keywords: macOS
---



**目录**

* TOC
{:toc}


## 设置macOS Terminal 命令自动完成
```
## Step 1 
sudo nano ~/.inputrc
## Step 2 - Paste the following commands one at a time
set completion-ignore-case on
set show-all-if-ambiguous on
TAB: menu-complete

## Step 3
Hit control+O to save changes to .inputrc followed by control+X to exit nano

## Step 4 Restart your shell OR
exec /bin/bash
```  
[参考链接1：](https://stackoverflow.com/questions/30958195/mac-terminal-auto-complete)  
[参考链接2：](http://osxdaily.com/2012/08/02/improve-tab-completion-in-mac-os-x-terminal/)


## 查询当前路径
[OpenClassroom](https://openclassrooms.com/en/courses/4614926-learn-the-command-line-in-terminal/4634361-create-your-first-directory)
```
pwd
```  

## 回到上级目录
```
cd ../
```

## 查询指定文件夹大小

```
du -hs /path/to/directory
```
-h is to get the numbers "human readable", e.g. get 140M instead of 143260 (size in KBytes)  
-s is for summary (otherwise you'll get not only the size of the folder but also for everything in the folder separately)
如果在恢复模式的话，这个命令无法使用，可以换成
```
ls -lh /path/to/directory
# -h是使得变成KB这种方式。
```


   
## 在恢复模式中的Terminal设置
  
默认在恢复模式里，是/private/var/root,我们先cd到用户名下

```
cd /Volumes/[硬盘名字]/Users/[用户名]
```

[复制CP命令](https://support.apple.com/en-hk/guide/terminal/apddfb31307-3e90-432f-8aa7-7cbc05db27f7/mac)

```
cp -R Desktop Documents/AAA
```
AAA这个文件夹不需要使用mkdir来创建，直接cp即可。

```
### mkdir 使用方法：
mkdir FileName
```

删除命令 - RM 删除Desktop内全部文件

```
rm /Volumes/Macintosh\ HD/Users/[UserName]/Desktop/*
```
或者
```
rm -v /Volumes/Macintosh\ HD/Users/[UserName]/Desktop/*
```
添加-v你可以看到哪些文件被删除。

## 权限问题

默认权限是归root的，因为是在恢复模式新增文件夹（也就是system)。  
<https://support.apple.com/en-hk/guide/mac-help/mchlp1038/mac>  
在复制好文件夹之后，可能产生权限问题，这个可以通过Get Info / CMD + I 解锁后进入Sharing & Permissions将用户加进去  

如果是从恢复模式直接通过代码添加则
```
## 先将文件夹所有者更改为该用户
sudo chown UserName -R path/to/directory 
sudo chmod -R 755 path/to/directory 
```
  
644代表，用户可读可写，用户组可读，其他组可读。
755代表，用户可读可写可执行，组可读可执行，其他可读可执行  
你也可以通过以下方式:  

```
sudo chmod u=rw,g=r,o=r path/to/directory

##或者 (755)
sudo chmod a+rwx,g-w,o-w path/to/directory
```
[命令转换网站](https://chmodcommand.com/chmod-755/)
  
下面是ls -l的解释：

```
-rw-r--r-- 12 linuxize users 12.0K Apr  8 20:51 filename.txt
|[-][-][-]-   [------] [---]
| |  |  | |      |       |
| |  |  | |      |       +-----------> 7. Group
| |  |  | |      +-------------------> 6. Owner
| |  |  | +--------------------------> 5. Alternate Access Method
| |  |  +----------------------------> 4. Others Permissions
| |  +-------------------------------> 3. Group Permissions
| +----------------------------------> 2. Owner Permissions
+------------------------------------> 1. File Type (如果开头是d代表这个是个文件夹)
```

