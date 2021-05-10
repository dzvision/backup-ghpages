---
layout: post
title: OpenWRT使用OpenClash翻阅
categories: OpenWRT
description: OpenWRT使用OpenClash翻阅
keywords: OpenWRT
---



我们将使用OpenWRT路由器通过旁路由的形式实现翻阅科学的过程。因为OpenWRT路由器软件储存不足，所以使用Extroot外接U盘的方式实现翻阅。


**目录**

* TOC
{:toc}

## OpenWRT查看本路由器储存状况

```
root@OpenWrt:~# df -h
```

## Extroot设置
[OpenWRT U盘储存教程](https://openwrt.org/docs/guide-user/additional-software/extroot_configuration)  
注意，请一行一行代码复制。  


## OpenWRT换源
例子：<https://mirrors.tuna.tsinghua.edu.cn/help/openwrt/>  
或者使用USTC源，注意手动换源请留意版本号。  

```
src/gz openwrt_core https://mirrors.ustc.edu.cn/openwrt/releases/19.07.6/targets/ramips/mt76x8/packages
src/gz openwrt_kmods https://mirrors.ustc.edu.cn/openwrt/releases/19.07.6/targets/ramips/mt76x8/kmods/4.14.215-1-d92769dc5268e102503ae83fe968a56c
src/gz openwrt_base https://mirrors.ustc.edu.cn/openwrt/releases/19.07.6/packages/mipsel_24kc/base
src/gz openwrt_freifunk https://mirrors.ustc.edu.cn/openwrt/releases/19.07.6/packages/mipsel_24kc/freifunk
src/gz openwrt_luci https://mirrors.ustc.edu.cn/openwrt/releases/19.07.6/packages/mipsel_24kc/luci
src/gz openwrt_packages https://mirrors.ustc.edu.cn/openwrt/releases/19.07.6/packages/mipsel_24kc/packages
src/gz openwrt_routing https://mirrors.ustc.edu.cn/openwrt/releases/19.07.6/packages/mipsel_24kc/routing
src/gz openwrt_telephony https://mirrors.ustc.edu.cn/openwrt/releases/19.07.6/packages/mipsel_24kc/telephony
```

## OpenClash配置  
1. 我们需要的依赖包如下安装：    
```
opkg update
opkg install luci luci-base iptables coreutils coreutils-nohup bash curl jsonfilter ca-certificates ipset ip-full iptables-mod-tproxy iptables-mod-extra ruby ruby-yaml kmod-tun luci-compat ip6tables-mod-nat
```

***************
以及需要：
dnsmasq-full
libcap
libcap-bin

需要注意的是，默认我们安装的是dnsmasq, 需要先Remove后，再安装dnsmasq-full。  

而libcap, libcap-bin在19.7版本中，去除了libcap-bin,导致会出现
“错误：Capsh异常，请尝试重新安装依赖【libcap】和相应的Capsh库，终止启动”  
具体可以参考[GitHub Issue](https://github.com/vernesong/openclash/issues/885) 里有具体描述。   

2. 正确做法是从<https://downloads.openwrt.org/snapshots/packages/mipsel_24kc/base/>下载libcap,libcap-bin安装。 （这两个要版本一致）  

你可以根据你自己的CPU构架选择自己的网址链接，我是mipsel_24kc的。

3. 安装后重启，即可在Service找到OpenClash并启用OpenClash