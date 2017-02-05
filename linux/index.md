---
layout: index 
title: "Linux"
---  
# Linux
{% for post in site.categories.life %}
- [{{ post.url }}]({{ post.title }})
{% endfor %}