---
layout: page
title: Blog
---

<ul class="toc">
    {% for post in site.posts %}
        <li>
            {{ post.date | date: "%Y/%m/%d" }} : <a href="{{ post.url }}">{{ post.title }}</a>
        </li>
    {% endfor %}
</ul>

[Voir les billets par thèmes](/blog/tags.html)
