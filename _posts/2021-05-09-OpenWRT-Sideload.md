---
layout: post
title: 使用OpenWRT旁路由模式与Ubiquiti(UBNT)对接
categories: OpenWRT
description: 使用OpenWRT旁路由模式用于VPN
keywords: OpenWRT
---



我们将使用OpenWRT路由器通过旁路由的形式实现翻阅科学的过程。


**目录**

* TOC
{:toc}

## 通过OpenWRT官网查找适配路由器
首先我们在OpenWRT官网，找到目前在更新并且直接能够刷机的可用路由器。
通过查询，我们最终选择GL-iNet这个国产品牌。(GL-MT300N V2)



## UBNT配置
1. Settings --> Networks 新建一个网络例如“Oversea”，定义Gateway IP为，例如10.10.10.1/25
2. 将DHCP Name Server修改为Manual, 并输入8.8.8.8+8.8.4.4
3. 将DHCP Gateway IP修改为手动并设置为10.10.10.2(旁路由的静态IP)
4. 保存
5. 配置交换机与OpenWRT路由器连接的口使用Profile为“Oversea”
6. 配置SSID Wifi，使用Profile为“Oversea”

## OpenWRT配置
[Zhihu Example](https://zhuanlan.zhihu.com/p/112484256)
1. 只需要配置LAN口为静态地址，并设置为10.10.10.2
2. IPv4 Gateway设置为10.10.10.1
3. DNS设置为8.8.8.8+8.8.4.4
4. 确保Physical Setting的Bridge interface打勾
5. DHCP Server设置为Ignore interface 打勾(也就是Disable DHCP)
6. 强制保存后，等待它到确认无法连接状态，将本路由器的Lan口网线与交换机连接。
7. 等待连接成功。
