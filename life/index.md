---
layout: index 
title: "日常"
---  
# 日常
{% for post in site.categories.life %}
- [{{ post.url }}]({{ post.title }})
{% endfor %}