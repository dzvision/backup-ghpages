---
layout: post
title: Windows IIS 10如何配置自签名SSL并实现自动跳转
categories: 网页服务器
description: 搭建Windows/Office KMS服务器
keywords: Windows,网页服务器
---

配置自签名难度不大，但是有一些坑路，所以在这里记录一下。  



**目录**

* TOC
{:toc}

## 1. 配置自签名的坑路
配置自签名，这里就不进行详细说明了。网上有大量的链接：
1. [Microsoft](https://docs.microsoft.com/en-us/iis/manage/configuring-security/configuring-ssl-in-iis-manager)  
2. [教程2](https://www.sslshopper.com/article-how-to-create-a-self-signed-certificate-in-iis-7.html)  
3. [Sophos](https://community.sophos.com/kb/en-us/132438)

在配置好443端口的时候，服务器可能会无法再次启动，原因搜索了一下，说是443端口被占用。其实解决方法是直接重启即可。
  
## 2. HTTP跳转HTTPS
使用中文搜索，得到的是很多年前的教程，实际上都不适用于IIS 10。
正确的做法是下载插件。

### 2.1 下载并安装URL Rewrite插件
下载地址: <https://www.iis.net/downloads/microsoft/url-rewrite>  
等待下载并安装好之后，需要退出一下IIS。因为这个时候IIS Manager里面URL Rewrite还没显示出来。
我们需要设置Web Config去修改。

### 2.2 设置Web Config
在你网站的根目录，有一个web.config的文件，把代码嵌入：
```
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
<system.webServer>
<rewrite>
<rules>
<rule name="Redirect to HTTPS" enabled="false" stopProcessing="true">
<match url="(.*)" />
<conditions><add input="{HTTPS}" pattern="^OFF$" />
</conditions>
<action type="Redirect" url="https://{HTTP_HOST}/{R:1}" redirectType="SeeOther" />
</rule>
</rules>
</rewrite>
</system.webServer>
</configuration>
```

由于我本来里面已经有配置，所以修改了一下：
```
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <system.webServer>
        <staticContent>
            <mimeMap fileExtension=".pkg" mimeType="application/macos" />
            <mimeMap fileExtension=".ipa" mimeType="application/ipad" />
        </staticContent>
        <directoryBrowse enabled="true" />
		<rewrite>
			<rules>
				<rule name="Redirect to HTTPS" enabled="true" stopProcessing="true">
					<match url="(.*)" />
					<conditions>
						<add input="{HTTPS}" pattern="^OFF$" />
					</conditions>
					<action type="Redirect" url="https://{HTTP_HOST}/{R:1}" redirectType="SeeOther" />
				</rule>
			</rules>
		</rewrite>
    </system.webServer>
</configuration>
```

如你所见，我之前通过MIME Types添加了pkg和ipa文件，这样用户访问就会直接下载，而不会是报错。
现在我又添加了HTTPS自动跳转。

### 2.3 IIS Manager查看效果
![URL Rewrite](/blog/images/posts/2020/IISManagerHTTPSredirect1.png)
现在，你只需要进入URL Rewrite并点击“Redirect to HTTPS”然后Enable Rule即可。

### 2.4 注意IIS早期版本教程导致坑路
记得在SSL Setting里面，不要勾选Require SSL!
否则会返回403.4错误。
![SSL Setting - Not Require](/blog/images/posts/2020/IISManagerHTTPSredirect2.png)




## 参考文献
参考文献1. [Namecheap](https://www.namecheap.com/support/knowledgebase/article.aspx/9953/38/iis-redirect-http-to-https)  

参考文献2. [Grid Scale](https://gridscale.io/en/community/tutorials/iis-redirect-http-to-https-windows/)