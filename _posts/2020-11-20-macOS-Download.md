---
layout: post
title: 如何指定下载不同版本macOS app
categories: macOS
description: 
keywords: macOS
---

macOS下载除了使用Update / Mac App Store的下载之外，还可以通过命令直接下载你目前系统当前版本的mac OS，甚至如果你想下载pkg版本也是可以实现的。

**目录**

* TOC
{:toc}


## 通过命令下载指定版本macOS App
```
### 指定版本
sudo softwareupdate --fetch-full-installer --full-installer-version 10.15.7

### 下载最新版本
sudo softwareupdate --fetch-full-installer
```  
直接使用Terminal即可。不过使用这个模式，有时候可能报错，不过你一直等待，结果还是下载好的，也有可能下载失败的可能。


## 通过installinstallmacos.py下载
[GitHub](https://github.com/munki/macadmin-scripts)
```
./installinstallmacos.py --compress

# 使用compress可以直接变成DMG格式，不用的话是sparseimage格式。
```

## 采用进阶版scriptingosx制作的macOS PKG
[ScriptingOSX](https://scriptingosx.com/2020/11/deploying-the-big-sur-installer-application/)  
[GitHub](https://github.com/scriptingosx/fetch-installer-pkg)  

以前，我们通过pkgbuild的方式可以直接打包Install macOS App，但是macOS Big Sur是无法通过这个方式实现的，ScriptingOSX里面有具体解释。所以PKG安装，可以直接采用fetch-installer-pkg的方式下载并保存为PKG格式。

```
### 使用方法：
./fetch-installer-pkg.py
```

## 将macOS App安装成可启动U盘
```
sudo /Applications/Install\ macOS\ Big\ Sur.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume
```
