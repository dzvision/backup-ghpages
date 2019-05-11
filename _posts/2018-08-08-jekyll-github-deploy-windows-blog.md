---
layout: post
title: Jekyll搭建博客并部署到GitHub
categories: 网页服务器
description: 搭建博客
keywords: Web, Jekyll, GitHub, Blog, 静态网页
---

尝试过很多Windows搭建静态网页博客的方法，都是失败告终。试了几次Jekyll，这一次终于成功了。想把一些坑路分享一下。


**目录**

* TOC
{:toc}

## 1. 下载Jekyll for Windows并安装

### 下载Jekyll
Jekyll官网：https://jekyllrb.com/docs/windows/

Jekyll on Windows: https://rubyinstaller.org/

提示：Jekyll Windows安装器已经包含RubyGems，所以无需再次下载。

### 安装Jekyll
然后我们安装Ruby+Devkit,安装完成后，会出现cmd提醒你安装1,2,3
我们选择3，安装全部组件。(Mingw)  
友情提示：他会不断提示多次，其实只需要安装一次即可。

打开Windows开始菜单，并找到Start Command Prompt with Ruby，打开使用Ruby。  

在打算更新gem之前，建议把gem源更换为中国源。  
```
gem sources --remove https://rubygems.org/ 
gem sources -a https://gems.ruby-china.com/
```
或  
```
gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/
```
然后我们查看目前的源：
```
gem sources -l
# 确保只有 gems.ruby-china.com
```

更新Ruby gem
```
gem update
```

然后我们安装组件
```
gem install jekyll bundler
```

通过jekyll -v可以检测是否安装成功。  


### 时间设置
因为我们是直接参考复制别人的主题，所以这个步骤在Windows会稍微不一样。  
我们需要先安装tzinfo-data到Windows中才可以。
```
# Windows does not include zoneinfo files, so bundle the tzinfo-data gem
gem 'tzinfo-data', platforms: [:mingw, :mswin, :x64_mingw, :jruby]
```
在步骤3和4中，我们将详细介绍如何设置。


### 自动生成问题
auto-regeneration on Windows alone:

Jekyll uses the listen gem to watch for changes when the --watch switch is specified during a build or serve. While listen has built-in support for UNIX systems, it may require an extra gem for compatibility with Windows.

Add the following to the Gemfile for your site if you have issues with auto-regeneration on Windows alone:
```
gem 'wdm', '~> 0.1.1' if Gem.win_platform?
```

## 2. 下载主题
我使用的是[mzlogin](https://github.com/mzlogin/mzlogin.github.io)的主题。
直接下载解压到想要的位置即可。

## 3. 安装TZINFO-DATA
```
gem install tzinfo-data
```

## 4. 编辑gemfile
在下载好的主题文件找到Gemfile并编辑
添加
```
# Windows does not include zoneinfo files, so bundle the tzinfo-data gem
gem 'tzinfo-data', platforms: [:mingw, :mswin, :x64_mingw, :jruby]
```
即可。

## 5. 本地运行网站测试
新建网站项目
```
jekyll new myblog
#位置位于C:\Users\ABC\myblog\

//切换到工程目录，并开启服务
cd myblog

bundle exec jekyll serve
```
因为我们是复制主题到该目录，会出现bundle未安装错误。  
重新安装一下就可以了，有时候更新也可以。

```
#安装bundle
bundle install

#更新bundle
bundle update --bundler
```



## 6. 修改侧边栏
把主页中侧边栏的Repo修改成分类栏。
粗暴法：直接把sidebar-popular-repo删除，并复制一个副本sidebar-categories-nav.html且重命名为sidebar-popular-repo。

### 问题 / To Do List
1. sidebar-categories-nav.html的分类不可以通过点击筛选文章。
2. 修改为Tag样式

## 7. Push到GitHub中
手残党直接通过GitHub Windows Commit即可。


## 小提示
1. 直接在cmd输入d:更换盘符。输入cd d:\abc\def\更换文件夹  
2. 如果把文件放到xxx.github.io/blog内，则会出现Github Page不更新。原因是GitHub只会阅读Jekyll中xxx.github.io/_includes,而不会进入blog/_includes
导致。该问题是可以解决的。需要在Github上设置Github Page。

## 分享图标问题
问：如何删减分享链接、图标呢？  
答：分享图标采用的是https://github.com/overtrue/share.js  
可以通过编辑sns-share.html内容
```
<div class="share-component" data-disabled="google,twitter,facebook" data-description="Share.js - 一键分享到微博，QQ空间，腾讯微博，人人，豆瓣"></div>
```
禁用并设置分享描述。


你也可以通过
```
data-sites="twitter,qq,wechat,douban,weibo"
```
设置启用的分享链接