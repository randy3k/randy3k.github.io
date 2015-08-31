---
layout: page
title:
header: Welcome!
tagline: 
---

### About

> I am Randy Lai, an Asistant professor at the University of Maine, the Department of Mathematics and Statsitics. Previously obatined a PhD in Statistics from University of California, Davis in 2015, also M.Phil and Undergraduate degrees from The Chinese University of Hong Kong.

You can contact me via

- [randy.cs.lai@gmail.com](mailto:randy.cs.lai@gmail.com)
- [chushing.lai@maine.edu](mailto:chushing.lai@maine.edu)


### Recent Posts


<div class="list-group">
  {% for post in site.posts limit:5  %}
    <div class="list-group-item">
        <h5 class="list-group-item-heading"><a href="{{ post.url }}">{{ post.title }}</a></h5>
        {{ post.date | date: "%b %e, %Y" }}{% for tag in post.tags %}
        <a class="label label-success" href="{{ site.tags_path }}#{{ tag }}-ref">{{ tag }}</a>
        {% endfor %}
    </div>  
  {% endfor %}
</div>
