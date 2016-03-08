---
layout: page
title: Blog - billets par thème
---

{% for category in site.categories %}

{% capture category_name %}
    {{ category | first }}
{% endcapture %}

{{category_name}} ({{ site.categories[category_name] | size }})
---------------------------------------------------------------

<ul class="toc">
    {% for post in site.categories[category_name] %}
        <li>
            {{ post.date | date: "%Y/%m/%d" }} : <a href="{{ post.url }}">{{ post.title }}</a>
        </li>
    {% endfor %}
</ul>
{% endfor %}

[Voir tous les billets par ordre chronologique](/blog)