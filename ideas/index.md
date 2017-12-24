---
layout: default
title: Posts Describing Ideas that I have Had (or Heard and Liked)
category: idea
---

# Some Posts

{% for post in site.categories["idea"] %}
## {{ post.title }}
### {{ post.date | date_to_long_string }}
{{ post.excerpt }}
### <a href="{{ post.url }}" class="index-link">More...</a>

{% endfor %}
