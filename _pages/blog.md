---
layout: default
permalink: /teaching/
title: Teaching
nav: true
nav_order: 1
# pagination:
#   enabled: true
#   collection: posts
#   permalink: /page/:num/
#   per_page: 5
#   sort_field: date
#   sort_reverse: true
#   trail:
#     before: 1 # The number of links before the current page
#     after: 3 # The number of links after the current page
---

<div class="post">

{% assign blog_name_size = site.blog_name | size %}
{% assign blog_description_size = site.blog_description | size %}

{% if blog_name_size > 0 or blog_description_size > 0 %}

  <div class="header-bar">
    <h1>Courses</h1>
  </div>
{% endif %}


<ul class="post-list">

  {% if page.pagination.enabled %}
    {% assign postlist = paginator.posts %}
  {% else %}
    {% assign postlist = site.posts %}
  {% endif %}

  {% for post in postlist %}

  {% if post.external_source == blank %}
    {% assign read_time = post.content | number_of_words | divided_by: 180 | plus: 1 %}
  {% else %}
    {% assign read_time = post.feed_content | strip_html | number_of_words | divided_by: 180 | plus: 1 %}
  {% endif %}
  {% assign year = post.date | date: "%Y" %}
  {% assign tags = post.tags | join: "" %}
  {% assign categories = post.categories | join: "" %}

  <li>

  {% if post.thumbnail %}

  <div class="row">
        <div class="col-sm-9">
  {% endif %}
      <h3 class="post-title">{{ post.title }}</h3>
      <p>{{ post.description }}</p>
      <p class="post-meta">
        {% if post.external_source %}
        &nbsp; &middot; &nbsp; {{ post.external_source }}
        {% endif %}
      </p>
      <p class="post-tags">
        <a href="{{ year | prepend: '/blog/' | prepend: site.baseurl}}">
          <i class="fa-solid fa-calendar fa-sm"></i> {{ year }} </a>

          {% if tags != "" %}
          &nbsp; &middot; &nbsp;
            {% for tag in post.tags %}
            <a href="{{ tag | slugify | prepend: '/blog/tag/' | prepend: site.baseurl}}">
              <i class="fa-solid fa-hashtag fa-sm"></i> {{ tag }}</a>
              {% unless forloop.last %}
                &nbsp;
              {% endunless %}
              {% endfor %}
          {% endif %}

          {% if categories != "" %}
          &nbsp; &middot; &nbsp;
            {% for category in post.categories %}
            <a href="{{ category | slugify | prepend: '/blog/category/' | prepend: site.baseurl}}">
              <i class="fa-solid fa-tag fa-sm"></i> {{ category }}</a>
              {% unless forloop.last %}
                &nbsp;
              {% endunless %}
              {% endfor %}
          {% endif %}
      </p>

  {% if post.thumbnail %}

  </div>

  <div class="col-sm-3">
    <img class="card-img" src="{{post.thumbnail | relative_url}}" style="object-fit: cover; height: 90%" alt="image">
  </div>
  </div>
  {% endif %}
  </li>

  {% endfor %}

</ul>

{% if page.pagination.enabled %}
{% include pagination.liquid %}
{% endif %}

</div>
