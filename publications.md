---
inmenu: 1
layout: page
title: Publications
permalink: /publications/
plugins_dir: [jekyll-scholar]
---

[Bruce Rannala on Google Scholar]

<h3>{{ site.data.pub_sum_list.pub_sum_list_title }}</h3>
<ul>
   {% for item in site.data.pub_sum_list.docs %}
      <li><a href="{{ item.url }}" alt="{{ item.title }}">{{ item.title }}</a></li>
   {% endfor %}
</ul>

### All Papers

{% bibliography --file rannala  %}

[Bruce Rannala on Google Scholar]: https://scholar.google.com/citations?user=rgw5bacAAAAJ