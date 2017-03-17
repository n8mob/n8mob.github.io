---
layout: reference
title: 2009
---

## This is the Index for 2009

[Google](https://www.google.com/)

{% for post in site.posts %}
	{% capture year %}{{ post.date | date: "%Y" }}{% endcapture %}
		{% if year == "2009" %}
			[{{ post.title }}]({{ site.url }}{{ post.url }})
		{% endif %}
{% endfor %}
