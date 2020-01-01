---
layout: blog
published: true
title: 新闻快讯档案馆
apptitle: News Archives of ROCEYS 
description: News Archives of ROCEYS 【每天33秒观世界】在这里每天60秒读懂世界 每日快讯简报推送接口API
---
{% for post in site.posts %}
 {% if post.categories contains 'news' %}
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
