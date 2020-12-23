---
layout: page
title: About
description: 一个注重企业安全，实现符合审计要求的IT合规化的小透明
keywords: dzvision
comments: true
menu: 关于
permalink: /about/
---

我的信仰在空中飘扬：经国序民，正其制度。群之所为事无不成，众之所举业无不胜。  


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
