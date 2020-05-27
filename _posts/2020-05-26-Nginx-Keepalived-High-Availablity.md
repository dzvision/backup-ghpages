---
layout: post
title: 使用Nginx免费版与Keepalived实现高可用性High Availablity方案
categories: 网页服务器
description: 搭建Windows/Office KMS服务器
keywords: Windows,网页服务器
---

# 使用Nginx免费版与Keepalived实现高可用性High Availablity方案


**目录**

* TOC
{:toc}

我们可以首先参考一下
[CNBlog - Kevingrace](https://www.cnblogs.com/kevingrace/p/6138185.html)   
在实际上，我是用[RedHat Article 2](https://www.redhat.com/sysadmin/keepalived-basics)来做的。  
有一些需要首先配置好的要求可以看看Keepalived的文档   
<https://www.keepalived.org/doc/installing_keepalived.html>    

他还有另外两篇文章，可以稍微看一下，但是用处不是特别大。
[RedHat Article 1](https://www.redhat.com/sysadmin/ha-cluster-linux)
[RedHat Article 3](https://www.redhat.com/sysadmin/advanced-keepalived)

我测试的时候使用的是虚拟机上做的CentOS和宝塔，本身带有keepalive 1.3版本(2017)
建议放网站的时候区分一下Server 1和Server 2的内容方便你直观的看出。
其次是记得通过修改hosts文件达到访问宝塔内网站的目的。

因为采用
```
yum install -y keepalived
```
也是一个老的版本，所以我们应该是要下载最新版本的。
[Keepalived官网下载](https://www.keepalived.org/download.html)
在测试的时候，可以先确保老版本测试时OK的，
我测试过老版本的主从模式，防火墙没有做任何配置，确实可用。

## 更新Keepalived

```
wget https://www.keepalived.org/software/keepalived-2.0.20.tar.gz
OR
wget https://github.com/acassen/keepalived/archive/v2.0.20.tar.gz
#采用这个方式下载速度非常慢，建议先下载，如果本身电脑配置了IIS的话，
#可以将下载文件放到网站文件夹里，然后直接
wget http://192.168.2.1/keepalived-2.0.20.tar.gz

#直接下载并解压
curl --progress http://192.168.2.1/keepalived-2.0.20.tar.gz | tar xz
```


我们可以通过
```
which keepalived

return [root@localhost ~]$/usr/sbin/keepalived
#或者从
whereis -l keepalived 
```
查看得知，目前的keepalived的执行包是安装在/usr/sbin/下。而其他文件按照linux的方式分布在/usr/local的/bin;/sbin;/etc等位置。   
如果采用默认的./configure 是不会安装到这个位置的。   
所以我们需要做
```
./configure --prefix=/usr/local/
```
不要安装到/usr/local/keepalived，这是为了新建不同版本keepalived才需要这么做的，比如/usr/local/keepalived-2.0.20。另外一个原因是我们目前keepalived旧版本安装位置是/usr/local/  
你也可以先卸载keepalived之后安装到/usr/local/keepalived。
```
sudo yum remove keepalived
```
跟着教程做完make / sudo make install (不建议使用sudo make && make install)  


## 运行前准备
当我尝试使用systemctl enable keepalived以及systemctl start keepalived发现   
Can't open PID file /run/keepalived.pid (yet?) after start...tory   
这是因为我们其实需要在安装完成后，将安装好的文件夹复制到特定位置

```
# 拷贝执行文件 将我们刚刚config好的文件复制（覆盖）到usr/sbin里
cp /usr/local/sbin/keepalived /usr/sbin/

# 将keepalived配置文件拷贝到etc下
sudo cp /usr/local/etc/sysconfig/keepalived /etc/sysconfig/

# 原文 - 将初始化脚本拷贝到系统初始化目录下
# sudo cp /home/centos/keepalived-2.0.20/keepalived/etc/init.d/keepalived /etc/init.d/

将初始化脚本拷贝到系统初始化目录下（官网）
ln -s /etc/rc.d/init.d/keepalived.init /etc/rc.d/rc3.d/S99keepalived


#====================新版本不需要========================#
# 创建keepalived文件夹
mkdir /etc/keepalived/

# 将keepalived配置文件拷贝到etc下
cp /usr/local/keepalived-2.0.10/keepalived/etc/keepalived/keepalived.conf /etc/keepalived/
#====================新版本不需要========================#

# 添加可执行权限
chmod +x /etc/init.d/keepalived
```

然后可以
```
keepalived --version
```
查看版本

## 运行
```
systemctl start keepalived
systemctl status keepalived
systemctl stop keepalived
systemctl reload-daemon

##自启动
systemctl enable keepalived
```

## 最后
通过
ip -brief address show
查看Server2 VIP是否存在。
一般的，这个时候网站已经完成Nginx-Keepalived 主从模式设置。
主主模式其实只是在配置上添加多类似的VRRP Instance配置即可。


## 没怎么看的参考资料
1. Active-Passtive <https://www.cnblogs.com/kevingrace/p/6138185.html>
2. Active-Active <https://www.cnblogs.com/kevingrace/p/6146031.html>  
3. <https://docs.nginx.com/nginx/admin-guide/high-availability/ha-keepalived-nodes/>
4. <https://devops.ionos.com/tutorials/configuring-a-high-availability-nginx-plus-pair/>
5. <https://blog.csdn.net/l1028386804/article/details/52577875>
6. <https://www.centlinux.com/2018/08/keepalived-configure-floating-ip-centos-7.html>
7. <https://www.digitalocean.com/community/tutorials/how-to-set-up-highly-available-web-servers-with-keepalived-and-floating-ips-on-ubuntu-14-04>
8. <https://tecadmin.net/setup-ip-failover-on-ubuntu-with-keepalived/>