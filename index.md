---
layout: default
---

<ul>
  {{ site.pages | sort: 'title', 'last' }}
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>