---
title: "News"
layout: textlay
excerpt: "Macroecology Lab at Tohoku University."
sitemap: false
permalink: /allnews.html
---

# News

{% for article in site.data.news %}
<p> <b>{{ article.date }}</b> <br> {{ article.headline | markdownify | remove: '<p>' | remove: '</p>' }} </p>
{% endfor %}
