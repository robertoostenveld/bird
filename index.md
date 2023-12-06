---
title: BagIt Research Data (BIRD) repository
layout: default
---

# BagIt Research Data (BIRD) repository

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

## Radboud datasets

<ul>
{% for dataset in site.data.radboud.meta %}
{% assign meta = dataset[1] %}

{% assign datasetid = meta.CollectionIdentifier %}
{% assign authors = meta.Authors | join: "; " | default: "Unknown"  %}
{% assign pubdate = meta.PublicationDate | split: " " %}
{% assign pubdate = pubdate[0] | split: "-" %}
{% assign pubdate = pubdate[2] %}

{% if datasetid %}
<li>
{{ authors }} ({{ pubdate }}): <a href="{{ site.baseurl }}/radboud/{{ datasetid }}">{{ meta.Title }}</a> Version {{ meta.Version }}. {{ meta.Publisher }}. (dataset). {{ meta.PersistentURL }}
</li>
{% endif %}

{% endfor %}
</ul>

## Zenodo datasets

<ul>
{% for dataset in site.data.zenodo %}
{% assign meta = dataset[1] %}

{% assign authors = '' %}
{% for creator in meta.metadata.creators %}
{% assign authors = authors | append: '; ' | append: creator.person_or_org.name %}
{% endfor %}
{% assign authors = authors | remove_first: "; " %}

{% assign datasetid = meta['id'] %}

{% assign pubdate = meta.metadata.publication_date | split: "-" | first %}

<li>
{{ authors }} ({{ pubdate }}): <a href=""{{ site.baseurl }}/zenodo/{{ datasetid }}">{{ meta['metadata']['title'] }}</a> Version {{ meta.versions.index }}. Zenodo. (dataset). {{ meta.links.doi }}
</li>

{% endfor %}
</ul>

## OpenNeuro datasets

<ul>
{% for dataset in site.data.openneuro %}
{% assign meta = dataset[1] %}

{% assign authors = meta.author | join: "; " | default: "Unknown"  %}

<li>
{{ authors }} ({{ meta.year }}): <a href="{{ site.baseurl }}/openneuro/{{ meta.id }}">{{ meta.title }}</a>. OpenNeuro. (dataset). https://doi.org/{{ meta.doi }}
</li>

{% endfor %}
</ul>

## DataverseNL datasets

<ul>
{% for dataset in site.data.dataverse %}
{% assign datasetid = dataset[0] %}
{% assign meta = dataset[1].resource %}

{% assign doi = meta.identifier.__text %}

{% assign authors = '' %}
{% for creator in meta.creators.creator %}
{% assign authors = authors | append: '; ' | append: creator.creatorName %}
{% endfor %}
{% assign authors = authors | remove_first: "; " %}

<li>
{{ authors }} ({{ meta.publicationYear }}): <a href="{{ site.baseurl }}/dataverse/{{ datasetid }}">{{ meta.titles.title }}</a>. DataverseNL. (dataset). https://doi.org/{{ doi }}
</li>

{% endfor %}
</ul>

## 4TU datasets

<ul>
{% for dataset in site.data.4tu %}
{% assign datasetid = dataset[0] %}
{% assign meta = dataset[1].resource %}

{% assign doi = meta.identifier.__text %}

{% assign authors = '' %}
{% for creator in meta.creators.creator %}
{% assign authors = authors | append: '; ' | append: creator.creatorName %}
{% endfor %}
{% assign authors = authors | remove_first: "; " %}

<li>
{{ authors }} ({{ meta.publicationYear }}): <a href="{{ site.baseurl }}/4tu/{{ datasetid }}">{{ meta.titles.title }}</a>. 4TU.ResearchData. (dataset). https://doi.org/{{ doi }}
</li>

{% endfor %}
</ul>
