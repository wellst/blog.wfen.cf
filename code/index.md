---
layout: index 
title: "Code"
---
# Code 

{% for post in site.categories.life %}  
- [{{ post.title }}]({{ post.url }})
{% endfor %}