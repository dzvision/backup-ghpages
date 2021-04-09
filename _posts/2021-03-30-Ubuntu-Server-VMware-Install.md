---
layout: post
title: 在VMware环境安装Ubuntu Server中遇到的无法安装问题
categories: 服务器
description: 在VMware环境安装Ubuntu Server中遇到的无法安装问题
keywords: 服务器
---


我们项目最近在测试pihole dns, 所以想要安装Ubuntu Server测试，结果发现报错。

**目录**

* TOC
{:toc}



## 1.解决安装Ubuntu Server到最后一步报错
安装Ubuntu Server到最后一步报错
Sorry, there was a problem.  

从各个论坛收集情报，有的说是mirror导致的问题，结果我替换mirror并没有解决。有的说禁用网卡安装，我是通过禁用网卡实现安装的。
单单是尝试安装Ubuntu Server我就已经筋疲力尽了，根本没想到禁用网卡可以工作。
然而如果禁用了网卡，那么后期修改网卡配置就非常复杂，下面我就说一下如何修改网卡配置。


## 2.Ubuntu Server 网卡配置
[How to Configure Static IP Address on Ubuntu 18.04](https://linuxize.com/post/how-to-configure-static-ip-address-on-ubuntu-18-04/#:~:text=Configuring%20Static%20IP%20address%20on%20Ubuntu%20Desktop,-Setting%20up%20a&text=In%20the%20Activities%20screen%2C%20search,Click%20on%20the%20cog%20icon.&text=In%20%E2%80%9CIPV4%E2%80%9D%20Method%22%20section,IP%20address%2C%20Netmask%20and%20Gateway.)
  
自从17的某个版本之后，Ubuntu开始了使用netplan作为设置网卡的工具，这里面使用了YAML的语法。
你可以采用如下方式查看目前的配置


```
ls /etc/netplan
##出现如下配置文件
00-installer-config.yaml
```  
  
你可以编辑这个文件，或者采用新建文件的方式新建配置。
在此之前，你需要知道你网卡的名字

```
ip link
##输出
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
3: ens3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP mode DEFAULT group default qlen 1000
    link/ether 56:00:00:60:20:0a brd ff:ff:ff:ff:ff:ff
```  
你也可以通过ip a 或者老方法ifconfig -a的方式查看。
从这里我们知道我的网卡名字为ens3。
lo是默认网卡的Loopback配置，无需修改。
更多信息可以参考[Ubuntu Network Configuration](https://ubuntu.com/server/docs/network-configuration)的描述。


  
## 2.1新建配置

直接新建一个01-netcfg.yaml：
```
sudo nano /etc/netplan/01-netcfg.yaml
```  

动态IP:
```
network:
  version: 2
  renderer: networkd
  ethernets:
    ens3:
      dhcp4: yes

```
  
静态IP与固定DNS:
```
network:
  version: 2
  renderer: networkd
  ethernets:
    ens3:
      dhcp4: no
      addresses:
        - 192.168.121.199/24
      gateway4: 192.168.121.1
      nameservers:
          addresses: [8.8.8.8, 1.1.1.1]
```

renderer是NetworkManager / networkd二选一, networkd是Ubunter Server用的管理器。  

## 2.2 确认配置或保存
你可以通过
```
sudo netplan try 
#或者
sudo netplan apply
```  
测试确认配置，或直接保存。

## 2.3 查看配置
```
#查看ip
ip a

#查看DNS
systemd-resolve --status | grep Current

#查看全部DNS
systemd-resolve --status

``` 

