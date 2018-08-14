---
layout: post
title: HTC Incredible S G11 Radio 基带 | RUU
categories: Android
description: Android
keywords: Android, HTC
---
## 无线基带

刷无线和刷Recovery方法是一样的，  
1-下载附件  
2-得到一个“PG32IMG.zip”文件(如果不是这个名字，请重命名)  
3-将PG32IMG.zip复制到内存卡的根目录  
4-将手机完全关机（即关机后卸下电池重装）  
5-按住手机的音量下键不放，再按开机键  

第4和5步您可以灵活变换下操作方法为，开机状态下，长按关机键，弹出对话框，点重启手机，看到关机画面的时候按住音量下键，直至手机开机进入HBOOT界面  

6-手机进入HBOOT界面自动搜索内存卡的PG32IMG.zip刷机文件  
7-搜索到文件后出现以下英文  
```
--------------------------------------
Parsing...[SD ZIP]
[1]RADIO V2
Do you want to upate?（你确定要更新？）
<Vol UP> YES （按音量上键 确定）
<Vol DOWN> （按音量下键 取消）
--------------------------------------
```

8-按音量上键确定更新RADIO，更新完毕后出现以下英文
```
--------------------------------------
Parsing...[SD ZIP]
[1]RADIO V2 - OK
Update Complete...（更新完成）
Press <POWER> to reboot （请按<电源键>重启）
```

至此Radio刷新完毕，Radio刷新完毕之后别忘了把内存卡上的PG32IMG.zip删掉哦，如果不删掉的话对于新手之后的刷机步骤不方便.  

## 官方Rom RUU

From Froyo-based RUUs:(仅适用于Android2.2)  
From the 1.36.405.1 RUU:  
20.23.30.0802U_38.02.01.11  
md5: d7831564500a81971ec96bd84d168981  
From the 1.36.720.1 RUU:  
has the same radio as the 1.36.405.1 RUU  
From the 1.37.708.2 RUU:  
has the same radio as the 1.36.405.1 RUU  
From the 1.37.921.6 RUU:  
has the same radio as the 1.36.405.1 RUU  
From the 1.38.707.1 RUU:  
has the same radio as the 1.36.405.1 RUU  
From the 1.43.415.3 RUU:  
20.27.30.0802U_38.03.01.08  
md5: 936fef99309a136a2a978fc0e66048b4  
From the 1.46.669.1 RUU:  
20.23.30.0802U_38.02.01.17  
md5: 2b68f8de282d20c79fbed9391ac053fc  
From the 1.47.1400.2 RUU:  
20.28.30.0802U_38.03.01.18  
md5: bcfc3dbb47db4e99acd60d387c01d7bd  
From the 1.47.1400.3 RUU:  
20.28.30.0802U_38.04.01.07  
md5: eb83213f5a093a7baf7571409c9c2498  

From Gingerbread-based RUUs:(仅适用于Android2.3)  
From the 2.12.405.4 RUU:  
20.2803.30.085AU_3805.04.03.12  
md5: 9b4733ed670268491185e6ca40610c8c  
From the 2.12.405.7 RUU:  
20.2804.30.085AU_3805.04.03.22  
md5: 07e9af5646ce9942ee6e84184c0425b0  
From the 2.12.415.5 RUU:   
20.2805.30.085AU_3805.04.03.27  
md5: a0b11913e44b12ae0323aff6ed2eba2a  
From the 2.12.707.4 RUU:  
has the same radio as the 2.12.415.5 RUU  
From the 2.12.707.5 RUU:  
has the same radio as the 2.12.415.5 RUU  
From the 2.12.708.4 RUU:  
has the same radio as the 2.12.415.5 RUU  
From the 2.12.980.2 RUU:  
has the same radio as the 2.12.405.4 RUU  
From the 2.12.981.2 RUU:  
has the same radio as the 2.12.405.4 RUU  
From the 2.21.1010.4 RUU:  
has the same radio as the 2.12.415.5 RUU  
From the 2.21.1400.8 RUU:  
20.2808.30.085AU_3805.06.03.03  
md5: f727a2dae56fd64eeef525ebf64858f7  
From the 2.30.405.1 RUU:  
has the same radio as the 2.21.1400.8 RUU  
From the 2.32.1010.1 RUU:  
20.2810.30.085AU_3805.06.03.16  
md5: c8c0be410c97e9bf82cdad54d4da0ef4  
From the 2.33.669.2 RUU:  
has the same radio as the 2.32.1010.1 RUU  

2012.6.29查看发现Gingerbread没有更新。可能只等4.1了