---
layout: post
title: 如何让DMG转换为PKG做软件部署
categories: macOS
description: 
keywords: macOS
---


**目录**

* TOC
{:toc}

## 序
想要在苹果部署软件，如果不使用Munki的话，那就要Apple Remote Desktop来部署，软件的格式也必须是PKG的。
事实上，MDM也是只能用PKG的方式部署。

## 1. 
最早我们使用productbuild将未安装的软件解压为app, 然后进入app将里面的info.plist提取+app的方式转换为pkg;将安装好的软件通过pkgbuild转换为pkg.
https://www.jianshu.com/p/1f08fa975caf

```
sudo productbuild --product /users/david.yi/Documents/GoogleChrome/Info.plist --component /users/david.yi/Documents/GoogleChrome/GoogleChrome.app /Applications /users/david.yi/Documents/googlev80.pkg

sudo pkgbuild --component /Applications/EV3.app/ /Users/Xadmin/Documents/EV3.pkg
sudo pkgbuild --component /Users/Xadmin/Desktop/Install\ macOS\ Catalina.app/ /Users/Xadmin/Documents/Cata.pkg
```

但是后来再也安装不了了。

## 2. 改用quickpkg
quickpkg来源自[scriptingosx](https://scriptingosx.com/2016/01/introducing-quickpkg/),我们可以通过[Github](https://github.com/scriptingosx/quickpkg)下载。  
除了这个，还有其他类似的工具，例如[munki-pkg](https://github.com/munki/munki-pkg)和[Jamf介绍的Package工具](https://support.jamfschool.com/hc/en-us/articles/115002300893-How-to-build-packages-for-macOS)  







## 3. quickpkg安装
需要使用Git的方式下载的话，就要安装Xcode. 直接下载好解压的话就不用了。
```
cd ~/Downloads
git clone https://github.com/scriptingosx/quickpkg.git
cd quickpkg
```


## 4. quickpkg使用
```
./quickpkg ~/Downloads/googlechrome.dmg --output ~/Downloads
```


