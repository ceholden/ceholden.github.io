---
layout: page
title: Repositories

to_add: ['TSTools', 'landsat_preprocess', 'open-geo-tutorial', 'yatsm', 'image_compositor', 'MLRS']
---

{% if site.github.public_repositories %}
  {% assign sorted_repos = site.github.public_repositories | sort: "stargazers_count" %}
{% else %}
  This section will be filled in when we published on Github (because we'll have access to site.github.*).
{% endif %}

<div class="posts">
  {% for repo in sorted_repos reversed %}
  {% if page.to_add contains repo.name %}
    <div class="post">
    <h1 class="post-title">
      <a href="{{ repo.html_url }}">
      {{ repo.name }}
     </a>
    </h1>
    {{ repo.description }}
    </div>
  {% endif %}
  {% endfor %}
</div>
