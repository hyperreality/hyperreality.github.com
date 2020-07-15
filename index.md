---
layout: page
---

<span class="intro">Hi, welcome to my personal website. I enjoy solving puzzles, and most of my posts here are to do with cybersecurity, cryptography, and word games.</span>

<h3>Projects</h3>

<a href="https://cryptohack.org"><img src="/assets/projects/cryptohack.png" height="50%" width="50%" style="margin: 0px 10px 20px 0px; float: left;">
<b>CryptoHack</b></a> is a fun platform for learning cryptography through a series of interactive challenges.
<div style="clear: both;"></div>

<a href="https://codewordsolver.com"><img src="/assets/projects/codeword.png" height="50%" width="50%" style="margin: 0px 10px 20px 0px; float: left;">
<b>Codeword Solver</b></a> helps 75000 people solve newspaper word puzzle clues each month.
<div style="clear: both;"></div>

<a href="https://github.com/hyperreality/Poetry-Tools"><img src="/assets/projects/poetrytools.png" height="50%" width="50%" style="margin: 0px 10px 20px 0px; float: left;">
<b>Poetry Tools</b></a> is a Python library for analysing poetry which has been used in literature research and linguistics software.
<div style="clear: both;"></div>

<h3>Blog</h3>

{% for post in site.posts %}
<span class="date-home">({{ post.date | date: "%Y/%m" }})</span> [{{ post.title }}]({{ post.url }}) <br>
{% endfor %}
