---
layout: page
title: "Weebby Life"
subtitle: This is where I get talkative bout anime
css: "/assets/css/index.css"
share-img: /assets/img/edited.JPG
share-title: "Weebby Life"
share-description: "what are you talkin about, ANIMES dont required any description"
support_promo_box: true
cover-img:
  - "/assets/img/banner8.png" : "collage1"
  - "/assets/img/banner_original_1200.png" : "collage2"
  - "/assets/img/banner_villans1200_290.png" : "top anime villains"

---



<div class="list-filters">
  <a href="/" class="list-filter filter-selected" style="background-color:#944BFA;text-decoration: none;color:black;font-family:helvetical;font-size:20px;">All posts</a>
  <a href="/popular" class="list-filter"  style="background-color:#944BFA;text-decoration: none;color:black;font-family:helvetical;font-size:20px;">Most Popular</a>
  <a href="/tutorials" class="list-filter"  style="background-color:#944BFA;text-decoration: none;color:black;font-family:helvetical;font-size:20px;">Tutorials</a>
  <a href="/tags" class="list-filter"  style="background-color:#944BFA;text-decoration: none;color:black;font-family:helvetical;font-size:20px;">Index</a>
</div>




{% assign posts = paginator.posts | default: site.posts %}

<div class="posts-list">
  {% for post in site.tags.tutorial %}
  <article class="post-preview">

    {%- capture thumbnail -%}
      {% if post.thumbnail-img %}
        {{ post.thumbnail-img }}
      {% elsif post.cover-img %}
        {% if post.cover-img.first %}
          {{ post.cover-img[0].first.first }}
        {% else %}
          {{ post.cover-img }}
        {% endif %}
      {% else %}
      {% endif %}
    {% endcapture %}
    {% assign thumbnail=thumbnail | strip %}

    {% if site.feed_show_excerpt == false %}
    {% if thumbnail != "" %}
    <div class="post-image post-image-normal">
      <a href="{{ post.url | absolute_url }}" aria-label="Thumbnail">
        <img src="{{ thumbnail | absolute_url }}" alt="Post thumbnail">
      </a>
    </div>
    {% endif %}
    {% endif %}

    <a href="{{ post.url | absolute_url }}">
      <h2 class="post-title">{{ post.title }}</h2>

      {% if post.subtitle %}
        <h3 class="post-subtitle">
        {{ post.subtitle }}
        </h3>
      {% endif %}
    </a>

    <p class="post-meta">
      {% assign date_format = site.date_format | default: "%B %-d, %Y" %}
      Posted on {{ post.date | date: date_format }}
    </p>

    {% if thumbnail != "" %}
    <div class="post-image post-image-small">
      <a href="{{ post.url | absolute_url }}" aria-label="Thumbnail">
        <img src="{{ thumbnail | absolute_url }}" alt="Post thumbnail">
      </a>
    </div>
    {% endif %}

    {% unless site.feed_show_excerpt == false %}
    {% if thumbnail != "" %}
    <div class="post-image post-image-short">
      <a href="{{ post.url | absolute_url }}" aria-label="Thumbnail">
        <img src="{{ thumbnail | absolute_url }}" alt="Post thumbnail">
      </a>
    </div>
    {% endif %}

    <div class="post-entry">
      {% assign excerpt_length = site.excerpt_length | default: 50 %}
      {{ post.excerpt | strip_html | xml_escape | truncatewords: excerpt_length }}
      {% assign excerpt_word_count = post.excerpt | number_of_words %}
      {% if post.content != post.excerpt or excerpt_word_count > excerpt_length %}
        <a href="{{ post.url | absolute_url }}" class="post-read-more">[Read&nbsp;More]</a>
      {% endif %}
    </div>
    {% endunless %}

    {% if site.feed_show_tags != false and post.tags.size > 0 %}
    <div class="blog-tags">
      Tags:
      {% for tag in post.tags %}
      <a href="{{ '/tags' | absolute_url }}#{{- tag -}}">{{- tag -}}</a>
      {% endfor %}
    </div>
    {% endif %}

   </article>
  {% endfor %}
</div>

{% if paginator.total_pages > 1 %}
<ul class="pagination main-pager">
  {% if paginator.previous_page %}
  <li class="page-item previous">
    <a class="page-link" href="{{ paginator.previous_page_path | absolute_url }}">&larr; Newer Posts</a>
  </li>
  {% endif %}
  {% if paginator.next_page %}
  <li class="page-item next">
    <a class="page-link" href="{{ paginator.next_page_path | absolute_url }}">Older Posts &rarr;</a>
  </li>
  {% endif %}
</ul>
{% endif %}
