---
layout: page
title: Tags
permalink: /tags
---
{% assign rawtags = "" %}
{% for page in site.pages %}
    {% assign ttags = page.tags | join:'|' | append:'|' %}
    {% assign rawtags = rawtags | append:ttags %}
{% endfor %}
{% assign rawtags = rawtags | split:'|' | sort %}

{% assign tags = "" %}
{% for tag in rawtags %}
    {% if tag != "" %}
        {% if tags == "" %}
            {% assign tags = tag | split:'|' %}
        {% endif %}
        {% unless tags contains tag %}
            {% assign tags = tags | join:'|' | append:'|' | append:tag | split:'|' %}
        {% endunless %}
    {% endif %}
{% endfor %}

{% for tag in tags %}
<h2 id="{{ tag }}">{{ tag }}</h2>
<ul class="tags-expo-posts">
{% for somepage in site.pages %}
{% if somepage.tags contains tag %}
<li><a class="post-title" href="{{ site.baseurl }}{{ somepage.url }}"> {{ somepage.title }}</a></li>
{% endif %}
{% endfor %}
</ul>
{% endfor %}

<ul id="markdown-toc">
{% for tag in tags %}
<li><a href="#{{ tag }}">{{ tag }}</a></li>
{% endfor %}
</ul>