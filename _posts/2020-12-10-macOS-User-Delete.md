---
layout: post
title: 如何删除macOS用户
categories: macOS
description: 
keywords: macOS
---

当无法采用常规方式删除的时候，我们需要用命令的方式删除

**目录**

* TOC
{:toc}


## Terminal
```
sudo dscl . delete /Users/yourUserName
sudo rm -rf /Users/yourUserName
```  
[参考链接1：](https://apple.stackexchange.com/questions/310308/delete-a-standard-user-from-mac-os) 

## 出现eDS错误提示如何解决
delete status: eDSPermissionError  
DS Error: -14120 (eDSPermissionError)    
这是因为Secure Token的问题，解决方法如下：

```
sudo sysadminctl -adminUser FirstCreateUserName -adminPassword PASSWORD -secureTokenOn CurrentUserName -password PASSWORD

>>2020-07-21 14:15:34.072 sysadminctl[527:5170] - Done!
```

如果出现如下错误：
```
sysadminctl[1529:37416] setSecureTokenAuthorizationEnabled error Error Domain=com.apple.OpenDirectory Code=5101 "Authentication server refused operation because the current credentials are not authorized for the requested operation." UserInfo={NSLocalizedDescription=Authentication server refused operation because the current credentials are not authorized for the requested operation., NSLocalizedFailureReason=Authentication server refused operation because the current credentials are not authorized for the requested operation.}
```
则表示你要删除的那个用户是普通用户，请重新把Admin权限给他，再次删除即可。


[参考链接2：](http://www.aixperts.co.uk/?p=214)


