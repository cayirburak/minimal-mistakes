---
layout: archive
permalink: /kategoriler/
title: Kategoriler
---
<ul class="tag-box inline">
{% assign tags_list = site.categories %}  
  {% if tags_list.first[0] == null %}
    {% for tag in tags_list %} 
      <li><a href="#{{ tag }}">{{ tag | capitalize }} <span>{{ site.tags[tag].size }}</span></a></li>
    {% endfor %}
  {% else %}
    {% for tag in tags_list %} 
      <li><a href="#{{ tag[0] }}">{{ tag[0] | capitalize }} <span>{{"({tag[1].size})"}}</span></a></li>
    {% endfor %}
  {% endif %}
{% assign tags_list = nil %}
</ul>


{% assign sorted_categories = site.categories | sort {|left, right| left[0] <=> right[0]} %}
{% for tag in sorted_categories %}
  <h2 class='tag' id="{{ tag[0] }}">{{ tag[0] | capitalize }}</h2>
  <ul class="post-list">
    {% assign pages_list = tag[1] %}
    {% for post in pages_list %}
      {% if post.title != null %}
      {% if group == null or group == post.group %}
      <li><a href="{{ site.url }}{{ post.url }}">
          <span class="entry-date"><time datetime="{{ post.date | date_to_xmlschema }}" itemprop="datePublished">{{ post.date | date: "%B %d, %Y" }}</time></span>
          &bull;
          {{ post.title }}
        </a></li>
      {% endif %}
      {% endif %}
    {% endfor %}
    {% assign pages_list = nil %}
    {% assign group = nil %}
  </ul>
{% endfor %}

