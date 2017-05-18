---
layout: default
---

<ul>
  {% for post in site.posts %}
    <li>
      <h3><a href="{{ post.url }}">{{ post.title }}</a></h3> - ({{ post.date | date: "%m.%d.%Y" }})
      <p>{{ post.excerpt }}</p>
    </li>
  {% endfor %}
</ul>