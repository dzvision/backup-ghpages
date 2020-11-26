---
layout: post
title: 利用vlmcsd搭建KMS服务器
categories: Windows
description: 搭建Windows/Office KMS服务器
keywords: Windows, Office, KMS
---

一直很想去试试搭建KMS服务器，一直也没有时间。最近空闲下来，专门研究了一下，其实十分简单。
而且vlmcsd支持几乎所有操作系统作为KMS服务器。
通过搭建后，支持Windows, Office激活。


**目录**

* TOC
{:toc}

## 1. 搭建KMS服务端

首先需要一台 VPS，在上面搭建 vlmcsd 服务端

来源：https://github.com/Wind4/vlmcsd/releases/tag/svn1111

```
wget https://github.com/Wind4/vlmcsd/releases/download/svn1111/binaries.tar.gz
```

## 2. 解压并查看
```
tar -zxvf binaries.tar.gz
cd binaries/Linux/intel/static/
ls
```

例：默认wget下载的地址是/home/ubuntu

或者也可以通过预先下载到自己的电脑然后解压上传需要的文件即可。

## 3. 挑选适合自己系统的版本
我们能看到适配各个系统的版本，因为我们用Linux, 所以打开这个文件夹，而且基本都是Intel处理器。
找到vlmcsd-x64-musl-static 或vlmcsd-x86-musl-static（根据你 VPS 的系统为 x86 或 x64 系统而定）。

注意：Amazon AWS是64位

## 4. 修改权限
```
chmod u+x vlmcsd-x64-musl-static 
```

## 5. 运行
(可选，建议直接跳过该步骤)
```
./vlmcsd-x64-musl-static
```

## 6. 移动文件
通过宝塔移动或复制文件“vlmcsd-x64-musl-static”到/usr/bin内
并改名为kms。

## 7. 修改文件为可执行
```
chmod +x /usr/bin/kms
```
## 8. 启动服务
然后直接执行 kms 即可启动服务。

## 其他事项

### 侦听端口
这个服务侦听的端口是1688，可以输入以下命令查看运行状态：
```
Sudo netstat -ntpl
```

或通过sudo htop 进程管理器查看

如果你的 VPS 开启了 iptables ，记得开启 1688 端口的 tcp 传输：
```
iptables -I INPUT 5 -p tcp -m state --state NEW -m tcp --dport 1688 -j ACCEPT
```

### 开机自启
```
vi /etc/rc.local
```
vi,vim, nano都可以

输入/usr/bin/kms并回车
按:wq保存退出即可  

### 在Windows环境使用vlmcsd
vlmcsd-Windows-x86.exe 是KMS Server模拟软件  （或x64）  
vlmcs-Windows-x86.exe 是测试KMS Server是否能正常连接和使用。后面参数带上IP地址，就是检测该KMS是否正常。

我们通过记录本机ip (ipconfig)  
使用cmd打开vlmcsd-Windows-x86.exe即可。
测试本地KMS是否运行，然后即可在局域网内，激活其他电脑。

```
c:\kms>vlmcsd-Windows-x64.exe

## 本机验证
c:\kms>vlmcs-Windows-x64.exe

## 非本机验证
c:\kms>vlmcs-Windows-x64.exe 172.29.14.20

```

因为我们关闭程序后，就停止运行了。所以我们也可以在本地电脑添加自启动服务项。  
```
sc create KMSserver binPath= C:\Allthings\Tools\kms-server.exe start= auto
[SC] CreateService 成功
```
因为忘了修改显示名称，所以再写
```
sc config KMSserver displayName= KMS-Mi-Server
```
这样在服务项里面就可以找到啦。



### Windows激活
slmgr.vbs -upk 卸载现有Key  
ver | find "10.0.">nul && slmgr.vbs -ipk NPPR9-FWDCX-D2C8J-H872K-2YT43
输入新Key (Win 10 Ent的GLVK)  
slmgr.vbs -skms 34.219.129.62  
slmgr.vbs -ato  
激活完成。  
可通过slmgr.vbs -dlv查询激活状态。  
[Windows KMS密钥](https://docs.microsoft.com/en-us/windows-server/get-started/kmsclientkeys)  

### Windows激活遇到问题
slmgr.vbs 无法激活：
On a computer running Microsoft Windows non-core edition, run 'slui.exe 0x2a 0xC0000022' to display the error text.

这是由于采用WinPE内的Windows安装器安装导致的文件权限问题。
请直接到C:\Windows\System32\spp\store文件夹，在属性-->安全里面查看“组或用户名”的文件权限，然后手动添加NT SERVICE\sppsvc 并赋予了完全控制的权限即可。

### Windows 10 非激活密钥
Generic Product Keys for Windows 10
这个密钥可以升级系统，或在有数字许可证的情况下重新联网激活系统。
Windows 10 Pro	VK7JG-NPHTM-C97JM-9MPGT-3V66T
Windows 10 Enterprise	XGVPP-NMH47-7TTHJ-W3FW7-8HV2C
更多详情可[查看](https://www.winhelponline.com/blog/windows-10-generic-products-keys-list/)


### 激活Office
支持Office 2010/2013/2016
用管理员身份运行命令行

```
if exist "C:\Program Files (x86)\Microsoft Office\Office14\ospp.vbs" (cd "C:\Program Files (x86)\Microsoft Office\Office14") else (cd "c:\Program Files\Microsoft Office\Office14")
if exist "C:\Program Files (x86)\Microsoft Office\Office15\ospp.vbs" (cd "C:\Program Files (x86)\Microsoft Office\Office15") else (cd "c:\Program Files\Microsoft Office\Office15")
if exist "C:\Program Files (x86)\Microsoft Office\Office16\ospp.vbs" (cd "C:\Program Files (x86)\Microsoft Office\Office16") else (cd "c:\Program Files\Microsoft Office\Office16")
cscript ospp.vbs /osppsvcauto
cscript ospp.vbs /sethst:34.219.129.62 (注意sethst:后面没有空格)
cscript ospp.vbs /act
cscript ospp.vbs /dstatus
```

激活完成。

### 激活服务器列表
```
kms.v0v.bid
kms.03k.org
kms.moeclub.org
########高校KMS#######
南安普顿大学：kms.soton.ac.uk
华盛顿大学：mskms.cac.washington.edu
佛罗里达州立大学：fsu-kms-01.fsu.edu
圭尔夫大学: activate.cfs.uoguelph.ca
国立交通大学：kmserv.nctu.edu.tw
國立宜蘭大學：kms.niu.edu.tw
實踐大學：kms.usc.edu.tw
东吴大学：kms.scu.edu.tw
苏州大学：kms.suda.edu.cn
中国科学技术大学：kms.ustc.edu.cn
南京航空航天大学：kms.nuaa.edu.cn
中山大学：kms.sysu.edu.cn  
上海交通大学：kms.sjtu.edu.cn
武汉理工大学：kms.whut.edu.cn
华北电力大学：202.204.74.218
华南理工大学：act.msweb.scut.edu.cn
北京大学：kms.pku.edu.cn
清华大学：kms.cic.tsinghua.edu.cn
复旦大学：mvls.fudan.edu.cn
同济大学：kms.tongji.edu.cn
上海财经大学：kms.shufe.edu.cn
上海师范大学：mskms.shnu.edu.cn
上海海事大学：kms.shmtu.edu.cn
南京航空航天大学：kms.nuaa.edu.cn
上海第二工业大学：kms.sspu.edu.cn
中国科学技术大学：kms.ustc.edu.cn
南京特殊教育师范学院：kms.njty.edu.cn
```

## 参考文献
1. [imeiji GitHub](https://imeiji.github.io/2018/02/08/%E5%88%A9%E7%94%A8vlmcsd%E6%90%AD%E5%BB%BAKMS%E6%BF%80%E6%B4%BB%E6%9C%8D%E5%8A%A1%E5%99%A8/)  
2. [lvmoo](https://wwww.lvmoo.com/517.love)
