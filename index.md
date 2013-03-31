---
layout: page
title: 神棍工作室
tagline: 神棍是一种生活态度
---
{% include JB/setup %}

神棍工作室成立于天朝六十一年；

某人不才，正是神棍工作室会长；

神棍是迷路的人用来指点目标的一种无奈的方法，人们不到山穷水尽的时候是不会使用的；


##文章列表：

---

<ul class="posts">
{% for post in site.posts %}
<li>
    <span>{{ post.date | date: "%Y-%m-%d" }}</span> &raquo;
    <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a>
    {% if post.author %}
    <i title="作者：{{post.author}}" class="icon-user"></i>
    {% endif %}
    {% if post.sourcecode %}
        <i title="有源码" class="icon-list-alt"></i>
    {% endif %}
    {% if post.lasttime %}
    <i title="最后修改时间：{{post.lasttime | date: "%Y-%m-%d"}}" class="icon-pencil"></i>
    {% endif %}
</li>
{% endfor %}
</ul>
