---
layout: default
title: Posts Transcribed from Other Media
category: transcribed
---

# Some Posts

{% for post in site.categories["transcribed"] %}
## {{ post.title }}
### {{ post.date | date_to_long_string }}
{{ post.excerpt }}
### <a href="{{ post.url }}" class="index-link">More...</a>

{% endfor %}



