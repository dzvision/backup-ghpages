---
layout: post
title: 如何使用Munki部署macOS软件
categories: macOS
description: 
keywords: macOS, Munki
---


**目录**

* TOC
{:toc}

## 序
macOS 可以通过MDM的方式进行管理，再加上注册Apple School Manager/Apple Business Manager的方式来注册设备  
即可实现近乎零接触部署。由于我们学校使用的是Mosyle，ASM/ABM只支持App Store的部署，而且Mosyle付费版才包含pkg部署。  
这里通过Munki的部署来实现这个功能。例如谷歌浏览器，VLC等。  

## 安装Munki
自macOS 10.14之后, 用户无需macOS Server来部署Munki.下面我来演示一下。安装步骤  
去GitHub下载[Munki](https://github.com/munki/munki)
在安装里，可以选择自定义安装，并且取消安装Managed Software Center
![Munki Install Step 1](blog/images/posts/2019/munki1.png)



## Munki Server部署
参考自[GitHub Wiki](https://github.com/munki/munki/wiki/Demonstration-Setup)

# 步骤1
```
cd /Users/Shared/
mkdir munki_repo
mkdir munki_repo/catalogs
mkdir munki_repo/icons
mkdir munki_repo/manifests
mkdir munki_repo/pkgs
mkdir munki_repo/pkgsinfo
```   

# 步骤2
```
chmod -R a+rX munki_repo
```   

# 步骤3
```
sudo ln -s /Users/Shared/munki_repo /Library/WebServer/Documents/
# 把Apache服务器文件位置设置一个镜像链接到我们的repository
```

# 步骤4
```
sudo apachectl start
```   

# 步骤5
```
/usr/local/munki/munkiimport --configure
Repo URL (example: afp://munki.example.com/repo): file:///Users/Shared/munki_repo
pkginfo extension (Example: .plist): .plist
pkginfo editor (examples: /usr/bin/vi or TextMate.app): TextMate.app
Default catalog to use (example: testing): testing
Repo access plugin (defaults to FileRepo): <just hit return> #按回车即可
```   

# 步骤6
```
/usr/local/munki/munkiimport ~/Downloads/Firefox\ 70.0.dmg
========================
#下面的东西会一行一行出。
========================
           Item name: Firefox 
        Display name: Mozilla Firefox
         Description: Web browser from Mozilla
             Version: 61.0.2
            Category: Internet
           Developer: Mozilla
  Unattended install: False
Unattended uninstall: False
            Catalogs: testing    
Import this item? [y/n] y
Upload item to subdirectory path []: apps/mozilla
Path /Users/Shared/munki_repo/pkgs/apps/mozilla doesn't exist. Create it? [y/n] y
No existing product icon found.
Attempt to create a product icon? [y/n] y
Attempting to extract and upload icon...
Created icon: /Users/Shared/munki_repo/icons/Firefox.png
Copying Firefox 61.0.2.dmg to /Users/Shared/munki_repo/pkgs/apps/mozilla/Firefox 61.0.2.dmg...
Edit pkginfo before upload? [y/n]: y
Saving pkginfo to /Users/Shared/munki_repo/pkgsinfo/apps/mozilla/Firefox-61.0.2...
Rebuild catalogs? [y/n] y
Adding apps/mozilla/Firefox-61.0.2 to testing...

```    

# 步骤7 服务端设置客户接收manifest
```
/usr/local/munki/manifestutil 
Entering interactive mode... (type "help" for commands)
> new-manifest site_default
> add-catalog testing --manifest site_default
Added testing to catalogs of manifest site_default.
> add-pkg Firefox --manifest site_default
Added Firefox to section managed_installs of manifest site_default.
> exit
```   
如果你有额外的软件，只需要再添加add-pkg即可。   


# 步骤8 在客户端安装好后设置
```
sudo defaults write /Library/Preferences/ManagedInstalls SoftwareRepoURL "http://192.168.20.20/munki_repo"
```   

完成   