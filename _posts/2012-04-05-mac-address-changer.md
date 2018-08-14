---
layout: post
title: 免费MAC 地址修改器（无需重启）Technitium MAC Address Changer
categories: Windows
description: Windows软件
keywords: Windows, 软件
---

[Download From Official Website](https://technitium.com/tmac/index.html)   

Version: 6.0.3

Programmer: Shreyas Zare
System Requirements:Windows 2000/XP/Server 2003/Vista/Server 2008/7/Server 2008 R2/8 (Developer Preview)

Cost: FREEWARE

Technitium MAC Address Changer allows you to change (spoof) Media Access Control (MAC) Address of your Network Interface Card (NIC) irrespective to your NIC manufacturer or its driver. It has a very simple user interface and provides ample information regarding each NIC in the machine. Every NIC has a MAC address hard coded in its circuit by the manufacturer. This hard coded MAC address is used by windows drivers to access Ethernet Network (LAN). This tool can set a new MAC address to your NIC, bypassing the original hard coded MAC address. Technitium MAC Address Changer is a must tool in every security professionals tool box.

There are some famous, commercial tools available in the market for USD 39.99 to as much as USD 2499!, but Technitium MAC Address Changer is available for FREE. We don't charge for just changing a registry value! Also knowing how this works doesn't require extensive research as some commercial tool providers claim! Read how it works (below) for more details.

Features

Internet Protocol v6 (IPv6) support added.

Works on Windows 7 and Windows 8 (Developer Preview) for both 32-bit and 64-bit.

Automatic Update feature added to update software to latest available version.

Update network card vendors list feature allows you to download latest vendor data (OUI) from IEEE.org.

Enhanced network configuration presets with IPv6 support allow you to quickly switch between network configurations.

Command line options with entire software functionality available. You can select a preset from specified preset file to apply directly.

Issues in previous version ironed out.

How Does It Work ?

This software just writes a value into the windows registry. When the Network Adapter Device is enabled, windows searches for the registry value 'NetworkAddress' in the key HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\{4D36E972-E325-11CE-BFC1- 08002bE10318}\[ID of NIC e.g. 0001]. If a value is present, windows will use it as MAC address, if not, windows will use the hard coded manufacturer provided MAC address. Some Network Adapter drivers have this facility built-in. It can be found in the Advance settings tab in the Network Adapter's Device properties in Windows Device Manager.


How To Change MAC Address

1. Starting MAC address changer will list all available network adapters.

2. Select the adapter you want to change the MAC address. You will get the details of your selection below.

3. In the Information tab, find the Change MAC Address frame. Enter new MAC address in the field and click Change Now! button. You may even click Random MAC Address button to fill up a randomly selected MAC address from the vendor list available.

4. To restore the original MAC address of the network adapter, select the adapter, click Restore Original button in the Change MAC Address frame.

NOTE: This tool cannot change MAC address of Microsoft Network Bridge. Network Bridge will automatically use the original MAC address of the first NIC added into bridge with the first octet of MAC address set to 0x02.


