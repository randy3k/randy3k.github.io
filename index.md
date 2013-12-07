---
layout: page
title:
header: Welcome!
tagline: Randy Talks Dot Net
---

###About

I am Randy Lai, a PhD student in the Department of Statistics, University of California, Davis. Previously, I obtained my Master and Undergraduate degrees from CUHK, The Chinese University of Hong Kong. I was born in Hong Kong and I spent my childhood and teenage years in this prosperous city.

You can contact me via

- [randy.cs.lai@gmail.com](mailto:randy.cs.lai@gmail.com)
- [rcslai@ucdavis.edu](mailto:rcslai@ucdavis.edu)

###Computing

I taught myself HTML, PHP, MYSQL, Flash and Visual Basic in secondary school.  Later, I developed skill in C/C++ and R. Now, being a heavy R user, I also learning Python, CUDA and Obj-C. Moreover, I have great interests in web development such as jQuery, AJAX, Node.js and Rails.


### Recent Posts

<div class="list-group">
  {% for post in site.posts limit:5  %}
    <div class="list-group-item">
        <h5 class="list-group-item-heading"><a href="{{ post.url }}">{{ post.title }}</a></h5>
        {{ post.date | date: "%b %e, %Y" }}{% for tag in post.tags %}
        <a class="btn btn-default btn-xs" href="{{ site.tags_path }}#{{ tag }}-ref">{{ tag }}</a>
        {% endfor %}
    </div>  
  {% endfor %}
</div>