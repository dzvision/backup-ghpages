---
layout: post
title: 在Windows环境下使用Vercel部署静态网站
categories: 网页服务器
description: Vercel部署静态网站
keywords: 服务器
---

# 在Windows环境下使用Vercel部署静态网站
我想使用Vercel来部署静态网页，但是与此同时，我又不想通过Git的形式。那么如何在Windows环境下通过Vercel CLI来部署静态网页呢？


**目录**

* TOC
{:toc}

使用Vercel CLI就必须要npm, 我们可以首先先去下载NodeJS for Windows并安装
[OpenJS Windows](https://nodejs.org/dist/v14.17.0/node-v14.17.0-x64.msi)   
NodeJS其他额外组件不需要安装。

## Vercel CLI安装
安装Vercel
```
npm i -g vercel
```

本来我以为可以不放在C盘，即：我直接用Pycharm新建环境，再到里面输入上面的代码。
结果发现其实，都是安装到AppData里面 T_T


## Vercel CLI使用
<https://vercel.com/docs/cli>  
我目前在PyCharm新建的项目文件夹内放置了我的静态网页，并直接通过Termainal输入vercel直接上传。
如果你是通过cmd的话，需要先cd到对的文件夹之后再上传。  

直接输入vercel，就是preview, 你也可以通过vercel --prod实现直接放到production内。


### Vercel CLI登录
```
vercel

> >  No existing credentials found. Please log in:
? Enter your email or team slug: 
```


第一次使用会让你登录，无论你使用第三方如GitHub，还是Signin with Email都可以填写你的Email来进行验证。
它会通过发送邮件，你点击验证链接进行验证。  
```
We sent an email to example@example.com. Please follow the steps provided inside it and make sure the security code matches Delightful Meerkat.
> Success! Email confirmed
Congratulations! You are now logged in. In order to deploy something, run `vercel`.
```
  
### Vercel CLI上传网站文件

```
(venv) D:\PycharmProjects\examplewebsite>vercel
Vercel CLI 22.0.1
? Set up and deploy “D:\PycharmProjects\examplewebsite”? [Y/n] y
? Which scope do you want to deploy to? yourVercelAccountName
? Link to existing project? [y/N] n
? What’s your project’s name? examplewebsite
? In which directory is your code located? ./

```
通过以上设置，即可上传完成，并可以通过网页查看了。

