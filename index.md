---
layout: page
title: 神棍工作室
tagline: 神棍是一种生活态度
---
{% include JB/setup %}

神棍工作室成立于天朝六十一年；  
某人不才，正是神棍工作室会长；  
神棍是迷路的人用来指点目标的一种无奈的方法，人们不到山穷水尽的时候是不会使用的；  
神棍工作室以【玩】之名对待生活、工作、爱好；
分类列表:
-----
<ul class="tag_box inline">
  {% assign categories_list = site.categories %}
  {% include JB/categories_list %}
</ul>
-----
标签列表:
-----
<ul class="tag_box inline">
{% assign tags_list = site.tags %}
{% include JB/tags_list %}
</ul>
-----
文章列表:
-----
<ul class="posts">
{% for post in site.posts %}
<li><span>{{ post.date | date: "%Y-%m-%d" }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
{% endfor %}
</ul>
-----
