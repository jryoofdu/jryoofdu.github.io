---
layout: default
permalink: /teaching/
title: Courses
nav: true
nav_order: 1
display_categories: [FDU, BCIT]
---

<div class="projects">

{% assign blog_name_size = site.blog_name | size %}
{% assign blog_description_size = site.blog_description | size %}

{% if blog_name_size > 0 or blog_description_size > 0 %}

    <header class="post-header">
        <h1 class="post-title">{{ page.title }}</h1>
        <p class="post-description">{{ page.description }}</p>
    </header>
{% endif %}

{% if site.enable_project_categories and page.display_categories %}
  <!-- Display categorized projects -->
  {% for category in page.display_categories %}
  <a id="{{ category }}" href=".#{{ category }}">
    <h2 class="project-category">{{ category }}</h2>
  </a>
  {% assign categorized_projects = site.projects | where: "category", category %}
  {% assign sorted_projects = categorized_projects | sort: "importance" %}
  <ul class="project-list">
  {% for project in sorted_projects %}

  {% if project.external_source == blank %}
  {% assign read_time = project.content | number_of_words | divided_by: 180 | plus: 1 %}
  {% else %}
  {% assign read_time = project.feed_content | strip_html | number_of_words | divided_by: 180 | plus: 1 %}
  {% endif %}
  {% assign year = project.date | date: "%Y" %}
  {% assign tags = project.tags | join: "" %}
  {% assign categories = project.categories | join: "" %}
  {% assign seasons = project.season %}

    <li>

  {% if project.thumbnail %}

    <div class="row">
          <div class="col-sm-9">
    {% endif %}
        <h3 class="post-title">{{ project.title }}</h3>
        <!-- <p>{{ project.description }}</p> -->
        <p class="post-meta">
          {% if project.external_source %}
          &nbsp; &middot; &nbsp; {{ project.external_source }}
          {% endif %}
        </p>
        <p class="post-tags">
          {% for season in seasons %}
          <!-- <a href="{{ season.url }}" target="_blank">
            <i class="fa-solid fa-calendar fa-sm"></i> {{ season.name }}
          </a> -->
          <i class="fa-solid fa-calendar fa-sm"></i> {{ season.name }}
          {% unless forloop.last %}
            &nbsp; &middot; &nbsp;
          {% endunless %}
          {% endfor %}

          {% if tags != "" %}
          &nbsp; &middot; &nbsp;
            {% for tag in project.tags %}
            <a href="{{ tag | slugify | prepend: '/blog/tag/' | prepend: site.baseurl}}">
              <i class="fa-solid fa-hashtag fa-sm"></i> {{ tag }}</a>
              {% unless forloop.last %}
                &nbsp;
              {% endunless %}
              {% endfor %}
          {% endif %}
        </p>

  {% if project.thumbnail %}

    </div>

    <div class="col-sm-3">
      <img class="card-img" src="{{project.thumbnail | relative_url}}" style="object-fit: cover; height: 90%" alt="image">
    </div>
    </div>
    {% endif %}
    </li>

  {% endfor %}
  </ul>
  {% endfor %}

{% else %}

<!-- Display projects without categories -->

{% assign sorted_projects = site.projects | sort: "importance" %}

  <!-- Generate cards for each project -->

  <ul class="post-list">
  {% for project in sorted_projects %}

  {% if project.external_source == blank %}
  {% assign read_time = project.content | number_of_words | divided_by: 180 | plus: 1 %}
  {% else %}
  {% assign read_time = project.feed_content | strip_html | number_of_words | divided_by: 180 | plus: 1 %}
  {% endif %}
  {% assign year = project.date | date: "%Y" %}
  {% assign tags = project.tags | join: "" %}
  {% assign categories = project.categories | join: "" %}
  {% assign seasons = project.season %}

    <li>

  {% if project.thumbnail %}

    <div class="row">
          <div class="col-sm-9">
    {% endif %}
        <h3 class="post-title">{{ project.title }}</h3>
        <!-- <p>{{ project.description }}</p> -->
        <p class="post-meta">
          {% if project.external_source %}
          &nbsp; &middot; &nbsp; {{ project.external_source }}
          {% endif %}
        </p>
        <p class="post-tags">
          {% for season in seasons %}
          <!-- <a href="{{ season.url }}" target="_blank">
            <i class="fa-solid fa-calendar fa-sm"></i> {{ season.name }}
          </a> -->
          <i class="fa-solid fa-calendar fa-sm"></i> {{ season.name }}
          {% unless forloop.last %}
            &nbsp; &middot; &nbsp;
          {% endunless %}
          {% endfor %}

          {% if tags != "" %}
          &nbsp; &middot; &nbsp;
            {% for tag in project.tags %}
            <a href="{{ tag | slugify | prepend: '/blog/tag/' | prepend: site.baseurl}}">
              <i class="fa-solid fa-hashtag fa-sm"></i> {{ tag }}</a>
              {% unless forloop.last %}
                &nbsp;
              {% endunless %}
              {% endfor %}
          {% endif %}
        </p>

  {% if project.thumbnail %}

    </div>
    </div>
    {% endif %}
    </li>

  {% endfor %}
  </ul>
{% endif %}

</div>
