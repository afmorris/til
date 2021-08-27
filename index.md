---
layout: default
---

# Welcome!

These are my "Today I Learned" snippets. Inspired by [simonw/til](https://github.com/simonw/til).

# Categories

Hunt through the categories below. Note that if a TIL is in multiple categories, it'll show up under all of them.

{% assign matched = site.pages | where: "tags", "til" %}
{% assign not_draft = matched | where: "tags", "published" %}
{{ not_draft.size }} TIL so far. <a href="feed.xml">Atom feed here</a>.

{% assign sorted = site.category-list | sort %}
{% for category in sorted %}
## {{ category }}
<ul>
    {% for page in not_draft %}
      {% for tag in page.tags %}
          {% if tag == category %}
              <li><a href="{{ page.url }}">{{ page.title }}</a></li>
          {% endif %} <!-- tag match -->
      {% endfor %} <!-- tag -->
    {% endfor %} <!-- page -->
</ul>
{% endfor %} <!-- category -->