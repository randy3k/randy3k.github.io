---
layout: page
title:
header: Welcome!
tagline: Randy Talks Dot Net
---

###About

I am Randy Lai, a PhD student in the Department of Statistics, University of California, Davis. Previously, I obtained by Master and Undergraduate degrees from CUHK, The Chinese University of Hong Kong. I was born in Hong Kong and I spent my childhood and teenage years in this prosperous city.

You can contact me via

- [randy.cs.lai@gmail.com](mailto:randy.cs.lai@gmail.com)
- [rcslai@ucdavis.edu](mailto:rcslai@ucdavis.edu)

###Computing

I taught myself HTML, PHP, MYSQL, Flash and Visual Basic in secondary school.  Later, I developed skill in C/C++ and R. Now, being a heavy R user, I also learning Python, CUDA and Obj-C. Moreover, I have great interests in web development such as jQuery, ajax, Node.js and CSS.


### Recent Posts

<div class="list-group">
  {% for post in site.posts limit:3  %}
    {% capture this_year %}{{ post.date | date: "%Y" }}{% endcapture %}
    {% capture this_month %}{{ post.date | date: "%B" }}{% endcapture %}
    {% capture next_year %}{{ post.previous.date | date: "%Y" }}{% endcapture %}
    {% capture next_month %}{{ post.previous.date | date: "%B" }}{% endcapture %}
    <!-- <li class="list-group-item"><span>{{ post.date | date: "%b %e, %Y" }}</span>  <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li> -->
    <div class="list-group-item">
        <h5 class="list-group-item-heading"><a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></h5>
        {{ post.date | date: "%b %e, %Y" }}{% for tag in post.tags %}
        <a class="btn btn-default btn-xs" href="{{ BASE_PATH }}{{ site.JB.tags_path }}#{{ tag }}-ref">{{ tag }}</a>
        {% endfor %}
    </div>  
  {% endfor %}
</div>