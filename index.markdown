---
layout: home
title: CS Daily Dive
description: A modern blog covering computer science, technology, gadgets, and education.
---

<h1 class="page-heading">CS Daily Dive</h1>
<p class="lead">Daily insights into computer science, technology trends, programming, and tech education. Your source for staying updated in the fast-moving tech world.</p>

<!-- Controls Section -->
<div class="controls fade-in">
  <div class="search-box">
    <input type="text" class="search-input" placeholder="Search posts..." id="searchInput">
    <button class="search-button" onclick="searchPosts()">Search</button>
  </div>
  
  <select class="filter-dropdown" id="topicFilter">
    <option value="">All Topics</option>
    {%- for topic in site.topics -%}
    <option value="{{ topic.title | slugify }}">{{ topic.title }}</option>
    {%- endfor -%}
  </select>
</div>

<!-- Posts Grid -->
<div class="posts-section">
  <h2 class="post-list-heading fade-in">Recent Posts</h2>
  <div id="postsContainer" class="post-list-grid">
    {%- for post in site.posts limit:6 -%}
    <div class="post-card fade-in" data-topics="{{ post.topics | join: ',' | slugify }}">
      <div class="post-card-content">
        <div class="post-card-header">
          <h3 class="post-card-title">
            <a class="post-link" href="{{ post.url | relative_url }}">{{ post.title | escape }}</a>
          </h3>
          <p class="post-card-meta">
            <span class="post-date">{{ post.date | date: "%b %-d, %Y" }}</span>
            {%- if post.topics -%}
            <span class="post-topics">
              {%- for topic in post.topics -%}
                <span class="tag">{{ topic }}</span>
              {%- endfor -%}
            </span>
            {%- endif -%}
          </p>
        </div>
        <div class="post-card-excerpt">
          {{ post.excerpt }}
        </div>
      </div>
    </div>
    {%- endfor -%}
  </div>
</div>

<!-- Topics Section -->
{%- if site.topics.size > 0 -%}
<div class="topic-list">
  <h2 class="post-list-heading fade-in">Explore Topics</h2>
  <div class="topic-grid">
    {%- for topic in site.topics -%}
    <a href="{{ topic.url | relative_url }}" class="topic-card fade-in">
      <div class="topic-card-content">
        <div class="topic-card-header">
          <h3 class="topic-card-title">{{ topic.title }}</h3>
          <p class="topic-card-meta">
            <span class="topic-date">{{ topic.date | date: "%b %-d, %Y" }}</span>
          </p>
        </div>
        <div class="topic-card-description">
          {{ topic.description }}
        </div>
      </div>
    </a>
    {%- endfor -%}
  </div>
</div>
{%- endif -%}

<p class="rss-subscribe fade-in">subscribe <a href="{{ "/feed.xml" | relative_url }}">via RSS</a></p>

<script>
  // Search functionality
  function searchPosts() {
    const searchTerm = document.getElementById('searchInput').value.toLowerCase();
    const selectedTopic = document.getElementById('topicFilter').value;
    const posts = document.querySelectorAll('.post-card');
    
    posts.forEach(post => {
      const title = post.querySelector('.post-card-title').textContent.toLowerCase();
      const excerpt = post.querySelector('.post-card-excerpt').textContent.toLowerCase();
      const postTopics = post.getAttribute('data-topics');
      
      const matchesSearch = title.includes(searchTerm) || excerpt.includes(searchTerm);
      const matchesTopic = !selectedTopic || postTopics.includes(selectedTopic);
      
      if (matchesSearch && matchesTopic) {
        post.style.display = 'flex';
      } else {
        post.style.display = 'none';
      }
    });
  }
  
  // Filter by topic
  document.getElementById('topicFilter').addEventListener('change', function() {
    searchPosts(); // Reuse search function for combined filtering
  });
  
  // Real-time search
  document.getElementById('searchInput').addEventListener('input', function() {
    searchPosts();
  });
</script>
