---
layout: page
title: About
description: myifeng's Personal Blog
keywords: 李啧啧, myifeng
comments: true
menu: 关于
permalink: /about/
                            
---

> Action is the proper fruit of knowledge !

## Contact

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
