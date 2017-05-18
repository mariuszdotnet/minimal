---
layout: default
---

<ul>
  {% for post in site.posts | sort: 'title', 'first' %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>