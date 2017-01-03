---
layout: default
title: Gary Davis's Blog
---
# Hello
<div id="home">
  <h1>Blog Posts</h1>
  <ul class="posts">
    {% for post in site.posts %}
      <li>
         <a href="{{ post.url }}">{{ post.title }}</a>
         {{ post.excerpt }}
      </li>
    {% endfor %}
  </ul>
</div>
