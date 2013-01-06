---
layout: page
title: 神棍工作室
tagline: 神棍是一种生活态度
---
{% include JB/setup %}

<div class="row-fluid">
<div class="span8">

<p>
神棍工作室成立于天朝六十一年；
</p>
<p>
某人不才，正是神棍工作室会长；
</p>
<p>
神棍是迷路的人用来指点目标的一种无奈的方法，人们不到山穷水尽的时候是不会使用的；
</p>


<h2>文章列表:</h2>
<hr>

<ul class="posts">
{% for post in site.posts %}
<li>
    <span>{{ post.date | date: "%Y-%m-%d" }}</span> &raquo;
    <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a>
    {% if post.author %}
    <i title="作者：{{post.author}}" class="icon-user"></i>
    {% endif %}
    {% if post.lasttime %}
    <i title="最后修改时间：{{post.lasttime | date: "%Y-%m-%d"}}" class="icon-pencil"></i>
    {% endif %}
</li>
{% endfor %}
</ul>
</div>

<div class="span4">
<h3>分类列表:</h3>

<ul class="tag_box inline">
  {% assign categories_list = site.categories %}
  {% include JB/categories_list %}
</ul>

<hr>

<h3>标签列表:</h3>

<ul class="tag_box inline">
{% assign tags_list = site.tags %}
{% include JB/tags_list %}
</ul>
</div>
</div>
