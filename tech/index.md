---
layout: default
title: Main Page
---

<div class="home">

This is a blog with <b>no recent</b> posts with a <b>recent</b> (September 2011) migration from Mediawiki to Jekyll. It was partially an experiment and further to doing it I will probably use Wordpress instead for it long-term, so some things might not work correctly and will probably not get fixed for now.

<h1 class="page-heading">Tags by usage</h1>
<ul>
{% capture tags %}
  {% for tag in site.tags %}
    <li data-sort="{{ site.posts.size | minus: tag[1].size | prepend: '0000' | slice: -4, 4 }}">
       <a href="#{{ tag[0] }}">{{ tag[0] }}</a>  {{ tag[1].size }} posts
       <!-- <a href="/{{ site.tag_page_dir }}/{{ tag[0] | slugify: 'pretty' }}">{{ tag[0] }} <span>{{ tag[1].size }}</span></a> -->
    </li>
  {% endfor %}
{% endcapture %}
{{ tags | split:'</li>' | sort | join:'</li>' }}
</ul>


<h1 class="page-heading">Posts by tag</h1>
{% for tag in site.tags %}
  {% assign t = tag | first %}
  {% assign posts = tag | last %}

<a id="{{ t }}">{{ t }}</a>
<ul>
{% for post in posts %}
  {% if post.tags contains t %}
  <li>
    <a href="{{ post.url }}">{{ post.title }}</a>
    <span class="date">{{ post.date | date: "%d %B %Y" }}</span>
  </li>
  {% endif %}
{% endfor %}
</ul>
{% endfor %}


No tag set
<ul>
{% for post in site.posts %}
  {% if post.tags.size == 0 %}
  <li>
    <a href="{{ post.url }}">{{ post.title }}</a>
    <span class="date">{{ post.date | date: "%d %B %Y" }}</span>
  </li>
  {% endif %}
{% endfor %}
</ul>

  <h1 class="page-heading">'Recent' Posts (last 30 posts)</h1>
  For all posts: <a href="/tech/all-posts-by-date.html">Show all posts</a>

  <ul class="post-list">

      {% for post in site.posts limit:30 %}
      <li>
        <span class="post-meta">{{ post.date | date: "%d %B %Y" }}</span>

        <h2>
          <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
        </h2>
      </li>
    {% endfor %}

  </ul>

  <p class="rss-subscribe">subscribe <a href="{{ "/feed.xml" | prepend: site.baseurl }}">via RSS</a></p>

