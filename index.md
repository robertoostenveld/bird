---
title: BagIt Research Data (BIRD) repository
---

# BagIt Research Data (BIRD) repository

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

## Datasets

<ul>
{% for item in site.data %}
  
  {% assign collid = item[1].CollectionIdentifier %}
  {% assign authors = item[1].Authors | join: ", " | default: "Unknown"  %}
  {% assign pubdate = item[1].PublicationDate | split: " " %}
  {% assign pubdate = pubdate[0] | split: "-" %}
  {% assign pubdate = pubdate[2] %}

  {% if collid %}
    <li>
    {{ authors }} ({{ pubdate }}): <a href="/dataset/{{ collid }}">{{ item[1].Title }}</a> Version {{ item[1].Version }}. {{ item[1].Publisher }}. (dataset). {{ item[1].PersistentURL }}
    </li>
  {% endif %}

{% endfor %}
</ul>
