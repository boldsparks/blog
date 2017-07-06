---
layout: default
---


{% for post in site.posts %}

{% if post.link == null %}
<h2><a href="{{post.url}}">{{ post.title }}</a></h2>
<p class="meta"><a href="{{post.url}}">{{ post.date | date_to_string }}</a></p>
{% else %}
<h2><a href="{{post.link}}">{{ post.title }}</a></h2>
<p class="meta"><a href="{{post.url}}">{{ post.date | date_to_string }}</a></p>
{% endif %}

{{ post.content }}

{% endfor %}