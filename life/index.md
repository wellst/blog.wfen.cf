---
layout: index 
title: "日常"
---

日常的记录  


      {% for post in site.categories.life %}
          [{{ post.title }}]({{ post.url }})
      {% endfor %}