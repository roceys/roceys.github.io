---
layout: blog
published: true
title: 多媒体&流媒体档案馆
apptitle: Stream Media Archives of ROCEYS 
description: Stream Media Archives of ROCEYS 
---
{% for post in site.posts %}
 {% if post.categories contains 'media' %}
 <div class="container">
    <a href="{{ post.url | prepend: site.baseurl }}">
        <h2 class="post-title">
            {{ post.title }}
        </h2>
        {% if post.subtitle %}
        <h5 class="post-subtitle">
            {{ post.subtitle }}
        </h5>
        {% endif %}
    </a>
    <div class="post-content-preview">
        {{ post.content | strip_html | truncate:200 }}
    </div>

    <p class="post-meta">
        Posted by {% if post.author %}{{ post.author }}{% else %}{{ site.title }}{% endif %} on {{ post.date | date:
        "%Y/%m/%d" }}
    </p>
    </div>
    {% endif %}
{% endfor %}
