---
title: BagIt Research Data (BIRD) repository
---

# BagIt Research Data (BIRD) repository

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

## Radboud datasets

<ul>
{% for dataset in site.data.radboud.meta %}
{% assign item = dataset[1] %}

{% assign datasetid = item.CollectionIdentifier %}
{% assign authors = item.Authors | join: "; " | default: "Unknown"  %}
{% assign pubdate = item.PublicationDate | split: " " %}
{% assign pubdate = pubdate[0] | split: "-" %}
{% assign pubdate = pubdate[2] %}

{% if datasetid %}
<li>
{{ authors }} ({{ pubdate }}): <a href="/radboud/{{ datasetid }}">{{ item.Title }}</a> Version {{ item.Version }}. {{ item.Publisher }}. (dataset). {{ item.PersistentURL }}
</li>
{% endif %}

{% endfor %}
</ul>

## Zenodo datasets

<ul>
{% for dataset in site.data.zenodo %}
{% assign item = dataset[1] %}

{% assign authors = '' %}
{% for creator in item.metadata.creators %}
{% assign authors = authors | append: '; ' | append: creator.person_or_org.name %}
{% endfor %}
{% assign authors = authors | remove_first: "; " %}

{% assign datasetid = item['id'] %}

{% assign pubdate = item.metadata.publication_date | split: "-" | first %}

<li>
{{ authors }} ({{ pubdate }}): <a href="/zenodo/{{ datasetid }}">{{ item['metadata']['title'] }}</a> Version {{ item.versions.index }}. Zenodo. (dataset). {{ item.links.doi }}
</li>

{% endfor %}
</ul>

## OpenNeuro datasets

<ul>
{% for dataset in site.data.openneuro %}
{% assign item = dataset[1] %}

{% assign authors = item.author | join: "; " | default: "Unknown"  %}

<li>
{{ authors }} ({{ item.year }}): <a href="/openneuro/{{ item.id }}">{{ item.title }}</a>. OpenNeuro. (dataset). https://doi.org/{{ item.doi }}
</li>

{% endfor %}
</ul>

## DataverseNL datasets

<ul>
{% for dataset in site.data.dataverse %}
{% assign datasetid = dataset[0] %}
{% assign item = dataset[1].resource %}

{% assign doi = item.identifier.__text %}

{% assign authors = '' %}
{% for creator in item.creators.creator %}
{% assign authors = authors | append: '; ' | append: creator.creatorName %}
{% endfor %}
{% assign authors = authors | remove_first: "; " %}

<li>
{{ authors }} ({{ item.publicationYear }}): <a href="/dataverse/{{ datasetid }}">{{ item.titles.title }}</a>. DataverseNL. (dataset). https://doi.org/{{ doi }}
</li>

{% endfor %}
</ul>

## 4TU datasets

<ul>
{% for dataset in site.data.4tu %}
{% assign datasetid = dataset[0] %}
{% assign item = dataset[1].resource %}

{% assign doi = item.identifier.__text %}

{% assign authors = '' %}
{% for creator in item.creators.creator %}
{% assign authors = authors | append: '; ' | append: creator.creatorName %}
{% endfor %}
{% assign authors = authors | remove_first: "; " %}

<li>
{{ authors }} ({{ item.publicationYear }}): <a href="/4tu/{{ datasetid }}">{{ item.titles.title }}</a>. 4TU.ResearchData. (dataset). https://doi.org/{{ doi }}
</li>

{% endfor %}
</ul>
