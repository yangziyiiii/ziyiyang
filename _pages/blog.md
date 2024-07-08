---
layout: archive
permalink: /blog/
title: "Blogs"
author_profile: true
---



<ul>
{% for post in site.posts %}
  <li>
    <a href="{{ post.url | relative_url }}">{{ post.title }}</a> - <span>{{ post.date | date: "%B %d, %Y" }}</span>
  </li>
{% endfor %}
</ul>



<!-- <ul>
{% for post in site.posts %}
  <li>
    <a href="{{ post.url | relative_url }}">{{ post.title }}</a> - <span>{{ post.date | date: "%B %d, %Y" }}</span>
    {% if post.categories %}
      <br>
      <small>Categories: {% for category in post.categories %}<a href="/category/{{ category | slugify }}/">{{ category }}</a>{% unless forloop.last %}, {% endunless %}{% endfor %}</small>
    {% endif %}
  </li>
{% endfor %}
</ul> -->