---
title: "Macroecology Lab - Publications"
layout: gridlay
excerpt: "Macroecology Lab -- Publications."
sitemap: false
permalink: /publications/
---


# Publications

## Group highlights

**At the end of this page, you can find the [full list of publications](#full-list-of-publications).**

{% assign number_printed = 0 %}
{% for publi in site.data.publist %}

{% assign even_odd = number_printed | modulo: 2 %}
{% if publi.highlight == 1 %}

{% if even_odd == 0 %}
<div class="row">
{% endif %}

<div class="col-sm-6 clearfix">
 <div class="well">
  <pubtit>{{ publi.title }}</pubtit>
  <img src="{{ site.url }}{{ site.baseurl }}/images/pubpic/{{ publi.image }}" class="img-responsive" width="33%" style="float: left" />
  <p>{{ publi.description }}</p>
  <p><em>{{ publi.authors }}</em></p>
  <p><strong><a href="{{ publi.link.url }}">{{ publi.link.display }}</a></strong></p>
  <p class="text-danger"><strong> {{ publi.news1 }}</strong></p>
  <p> {{ publi.news2 }}</p>
 </div>
</div>

{% assign number_printed = number_printed | plus: 1 %}

{% if even_odd == 1 %}
</div>
{% endif %}

{% endif %}
{% endfor %}

{% assign even_odd = number_printed | modulo: 2 %}
{% if even_odd == 1 %}
</div>
{% endif %}

<p> &nbsp; </p>


## Full List of Publications
<ol reversed>
{% for publi in site.data.publist %}
  {% if publi.volume == "" %}
    {% if publi.early == 1 %}
      <li>{{ publi.authors }} <a href="{{ publi.link.url }}">{{ publi.title }}</a>. <em>{{ publi.journal }}</em>, Early Access.</li>
    {% endif %}
    {% if publi.preprint == 1 %}
      <li>{{ publi.authors }} <a href="{{ publi.link.url }}">{{ publi.title }}</a>. <em>{{ publi.journal }}</em>, Preprint.</li>
    {% endif %}
  {% else %}
    <li>{{ publi.authors }} ({{ publi.year }}). <a href="{{ publi.link.url }}">{{ publi.title }}</a>. <em>{{ publi.journal }}</em>, {{publi.volume}}: {{publi.issue}}, {{ publi.pages }}.</li>
  {% endif %}
{% endfor %}

