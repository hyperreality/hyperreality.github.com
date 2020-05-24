---
layout: page
---

<span class="intro">Hi, welcome to my personal website. I enjoy solving puzzles, and most of my posts here are to do with cybersecurity, cryptography, and word games.<br /><br /></span>

{% for post in site.posts %}
<span class="date-home">({{ post.date | date: "%Y/%m" }})</span> [{{ post.title }}]({{ post.url }}) <br>
{% endfor %}
