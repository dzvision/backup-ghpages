---
layout: post
title: Nginx 80端口导致无法启动的问题
categories: 网页服务器
description: 重启服务器后，宝塔Web出现问题
keywords: nginx
---

## 解决nginx: [emerg] bind() to [::]:80 failed (98: Address already in use)

**目录**

* TOC
{:toc}

## 查看端口占用
应该首先查看端口占用情况，并尝试杀进程

```
sudo netstat -ntpl
（并非所有进程都能被检测到，所有非本用户的进程信息将不会显示，如果想看到所有信息，则必须切换到 root 用户）
激活Internet连接 (仅服务器)
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address               Foreign Address             State       PID/Program name   
tcp        0      0 0.0.0.0:3306                0.0.0.0:*                   LISTEN      21539/mysqld        
tcp        0      0 0.0.0.0:80                  0.0.0.0:*                   LISTEN      1473/nginx          
tcp        0      0 0.0.0.0:8081               0.0.0.0:*                   LISTEN      15111/python        
tcp        0      0 0.0.0.0:21                  0.0.0.0:*                   LISTEN      27845/pure-ftpd (SE 
tcp        0      0 0.0.0.0:888                 0.0.0.0:*                   LISTEN      1473/nginx          
tcp        0      0 127.0.0.1:25                0.0.0.0:*                   LISTEN      1199/master         
tcp        0      0 0.0.0.0:1023               0.0.0.0:*                   LISTEN      3819/sshd 
```
然后根据PID 例如1473 监听了80和888端口 进行kill 
在ubuntu中  应使用如下命令行
```
sudo kill 1473
```
或者通过
```
sudo killall -9 nginx
#killall [options] program_name(s)
```

之后通过
```
sudo service nginx restart
```

重启进程

实际使用中，应直接使用宝塔面板启动即可。


### 题外话
另外，由于默认设置对ipv6的问题也有可能导致该错误的发生。 
解决方案是编辑nginx的配置文件
```
sudo vim /etc/nginx/sites-available/default
```
修改这一段：
```
listen 80; 
listen [::]:80 default_server; 
```
为
```
listen 80; 
listen [::]:80 ipv6only=on default_server; 
```
然后启动nginx，完美解决！