---
layout: page
title: Blog
permalink: /blog/
---

# Engineering Log

Short deep dives into backend performance optimization, high-variability data processing, and technical lessons learned from system builds.

## Recent Logs
{% for post in site.posts %}
* **{{ post.date | date: "%b %d, %Y" }}** — [{{ post.title }}]({{ post.url }})
{% else %}
*No logs published yet. First entry coming shortly.*
{% endfor %}