---
layout: page
title: About
description: 书写自己的传奇
keywords: 我是谁
comments: true
menu: 关于
permalink: /about/
---

听雪，听萧，听雨，却发现原来一直我都是擦肩而过的行人。

## 联系

{% for website in site.data.social %}
* {{ website.sitename }}：[@{{ website.name }}]({{ website.url }})
{% endfor %}

## Skill Keywords

{% for category in site.data.skills %}
### {{ category.name }}
<div class="btn-inline">
{% for keyword in category.keywords %}
<button class="btn btn-outline" type="button">{{ keyword }}</button>
{% endfor %}
</div>
{% endfor %}
