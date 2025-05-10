---
layout: archive
title: "Sitemap"
permalink: /sitemap/
author_profile: true
---

{% include base_path %}

A list of all the posts and pages found on the site. For you robots out there, there is an [XML version]({{ base_path }}/sitemap.xml) available for digesting as well.

{% assign visible_pages = site.pages | where_exp: "page", "page.sitemap != false" %}
{% if visible_pages.size > 0 %}
<h2>Pages</h2>
  {% for page in visible_pages %}
    {% include archive-single.html %}
  {% endfor %}
{% endif %}

{% assign visible_posts = site.posts | where_exp: "post", "post.sitemap != false" %}
{% if visible_posts.size > 0 %}
<h2>Posts</h2>
  {% for post in visible_posts %}
    {% include archive-single.html %}
  {% endfor %}
{% endif %}

{% capture written_label %}'None'{% endcapture %}

{% for collection in site.collections %}
  {% assign visible_collection_items = collection.docs | where_exp: "item", "item.sitemap != false" %}
  {% unless collection.output == false or collection.label == "posts" or visible_collection_items.size == 0 %}
    {% capture label %}{{ collection.label }}{% endcapture %}
    {% if label != written_label %}
      <h2>{{ label }}</h2>
      {% capture written_label %}{{ label }}{% endcapture %}
    {% endif %}
    {% for item in visible_collection_items %}
      {% include archive-single.html %}
    {% endfor %}
  {% endunless %}
{% endfor %}
