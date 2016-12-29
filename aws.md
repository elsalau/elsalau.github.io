---
layout: page
title: AWS
permalink: /aws/
---

<div class="aws">

  <h1 class="page-heading">AWS</h1>

  <ul class="post-list">
    {% for post in site.posts %}
      {% if post.categories contains "aws" %}
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
