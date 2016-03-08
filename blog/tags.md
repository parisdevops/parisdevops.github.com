---
layout: page
title: Blog - billets par thème
---

{% for category in site.categories %}

{% capture category\_name %}
    {{ category | first }}
{% endcapture %}

{{category\_name}} ({{ site.categories[category\_name] | size }})
-----------------------------------------------------------------

<ul class="toc">
    {% for post in site.categories[category\_name] %}
        <li>
            {{ post.date | date: “%d/%m/%Y” }} : <a href="{{ post.url }}">{{ post.title }}</a>
        </li>
    {% endfor %}
</ul>
{% endfor %}

[Voir tous les billets par ordre chronologique](/blog)
