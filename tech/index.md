---
layout: default
---

<div class="home">

  <h1 class="page-heading">Posts</h1>

  <ul class="post-list">

    {% assign sorted = site.posts | sort: 'date' | reverse %}
    {% for post_sorted in sorted %}
  <li>
        <span class="post-meta">{{ post_sorted.date | date: "%d %B %Y %H:%M:%S" }}</span>

        <h2>
          <a class="post-link" href="{{ post_sorted.url | prepend: site.baseurl }}">{{ post_sorted.title }}</a>
        </h2>
      </li>
    {% endfor %}

  
  </ul>

  <p class="rss-subscribe">subscribe <a href="{{ "/feed.xml" | prepend: site.baseurl }}">via RSS</a></p>

</div>
