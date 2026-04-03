---
layout: home
title: CS Daily Dive
description: A modern blog covering computer science, technology, gadgets, and education.
---

<div class="home">

  <h1 class="page-heading">CS Daily Dive</h1>

  <p class="lead">Daily insights into computer science, technology trends, programming, and tech education. Your source for staying updated in the fast-moving tech world.</p>

  <h2 class="post-list-heading">Recent Posts</h2>

  <ul class="post-list">
    {% for post in site.posts limit:3 %}
      <li>
        <span class="post-meta">{{ post.date | date: "%b %-d, %Y" }}</span>

        <h3>
          <a class="post-link" href="{{ post.url | relative_url }}">{{ post.title | escape }}</a>
        </h3>
        {{ post.excerpt }}
      </li>
    {% endfor %}
  </ul>

  <p class="rss-subscribe">subscribe <a href="{{ "/feed.xml" | relative_url }}">via RSS</a></p>

</div>
