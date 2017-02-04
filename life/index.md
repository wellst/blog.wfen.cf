---
layout: index
title： "日常"
---

日常的记录
    <ul>
      {% for post in site.categories.life %}
        <li>
          <span class="label label-info">{{ post.categories}}</span><a href="{{ post.url }}">{{ post.title }}</a>
        </li>
      {% endfor %}
    </ul>