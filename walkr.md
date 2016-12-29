---
layout: page
title: Walkr
permalink: /walkr/
---

<div class="rails">

  <h1 class="page-heading">Walkr</h1>

  <ul class="post-list">
    {% for post in site.posts %}
      {% if post.categories contains "walkr" %}
      <li>
        <span class="post-meta">{{ post.date | date: "%b %-d, %Y" }}</span>

        <h2>
          <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title | escape }}</a>
        </h2>
      </li>
      {% endif %}
    {% endfor %}
  </ul>

  <p class="rss-subscribe">subscribe <a href="{{ "/feed.xml" | prepend: site.baseurl }}">via RSS</a></p>

</div>
