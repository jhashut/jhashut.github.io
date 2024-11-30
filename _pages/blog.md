---
layout: default
permalink: /blog/
title: blog
nav: true
nav_order: 1
pagination:
  enabled: false
  collection: posts
  permalink: /page/:num/
  per_page: 5
  sort_field: date
  sort_reverse: true
  trail:
    before: 1 # The number of links before the current page
    after: 3 # The number of links after the current page
---

<div class="post">
  <h1 class="font-weight-bold">📝 Curiously Clueless!</h1>
  <h5 class="font-weight-lighter">Subscribe to my rants on <a href="https://curiouslyclueless.substack.com/"> Substack </a></h5>

  <table class="table">
    <thead>
      <tr>
        <th>Date</th>
        <th>Title</th>
        <th>Tags</th>
      </tr>
    </thead>
    <tbody>
      {% for post in site.posts %}
        <tr>
          <td>{{ post.date | date: "%d-%m-%Y" }}</td>
          <td>
            {% if post.redirect == blank %}
              <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
            {% elsif post.redirect contains '://' %}
              <a href="{{ post.redirect }}" target="_blank">{{ post.title }}</a>
            {% else %}
              <a href="{{ post.redirect | relative_url }}">{{ post.title }}</a>
            {% endif %}
          </td>
          <td>
            {% if post.tags %}
              {% for tag in post.tags %}
                {% assign hash = tag | hash %}
                {% assign hue = hash | modulo: 360 %}
                <a href="{{ tag | slugify | prepend: '/blog/tag/' | prepend: site.baseurl}}" 
                   class="badge" 
                   style="margin-right: 4px; background-color: hsl({{hue}}, 70%, 35%); color: white;">
                   {{ tag }}</a>
              {% endfor %}
            {% endif %}
          </td>
        </tr>
      {% endfor %}
    </tbody>
  </table>
</div>