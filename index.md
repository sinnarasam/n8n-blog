---
layout: page
title: 📋 AI 블로그 목록
---

{% assign sorted = site.data.posts | reverse %}
{% for post in sorted %}
### [{{ post.title }}]({{ post.url }})
📅 **{{ post.date }}**  |  🏷️ `{{ post.category }}`

---
{% endfor %}
