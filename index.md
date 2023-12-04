---
title: BagIt Research Data (BIRD) repository
---

# BagIt Research Data (BIRD) repository

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

## Zenodo datasets


<ul>
{% for item in site.data.zenodo %}

{% assign authors = '' %}
{% for creator in item[1].metadata.creators %}
  {% assign authors = authors | append: creator.person_or_org.name | append: '; ' %}
{% endfor %}
{% assign authors = authors | split: "" | reverse | join: "" | remove_first: ";" | split: "" | reverse | join: "" %}

{% assign collid = item[1]['id'] %}

{% assign pubdate = item[1].metadata.publication_date | split: "-" | first %}

<li>
{{ authors }} ({{ pubdate }}): <a href="/zenodo/{{ collid }}">{{ item[1]['metadata']['title'] }}</a> Version {{ item[1].versions.index }}. Zenodo. (dataset). {{ item[1].links.doi }}
</li>

{% endfor %}
</ul>

## Radboud datasets

<ul>
{% for item in site.data.radboud.meta %}

  {% assign collid = item[1].CollectionIdentifier %}
  {% assign authors = item[1].Authors | join: ", " | default: "Unknown"  %}
  {% assign pubdate = item[1].PublicationDate | split: " " %}
  {% assign pubdate = pubdate[0] | split: "-" %}
  {% assign pubdate = pubdate[2] %}

  {% if collid %}
    <li>
    {{ authors }} ({{ pubdate }}): <a href="/radboud/{{ collid }}">{{ item[1].Title }}</a> Version {{ item[1].Version }}. {{ item[1].Publisher }}. (dataset). {{ item[1].PersistentURL }}
    </li>
  {% endif %}

{% endfor %}
</ul>
