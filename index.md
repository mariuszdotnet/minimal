---
layout: default
---

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a> - ({{ post.date | date: "%m.%d.%Y" }})
      <br/>{{ post.excerpt }}
    </li>
  {% endfor %}
</ul>