---
title: BagIt Research Data (BIRD) repository
layout: default
---

This is a demonstration project inspired by the
[BagIt](https://en.wikipedia.org/wiki/BagIt) standard for storage
and network transfer of arbitrary digital content, including
research data.

With research datasets represented as "Bags" with metadata in
the `bag-info.txt` file, and the pointers to the actual data
files on a download server listed in the `fetch.txt` file,
writing a repository server becomes relatively simple. This project
is an exploration into such a research data repository server.

At this moment it only includes a few examples with the BagIt
metadata format; most of the examples here use various metadata
schemas from other repositories. In the future I can imagine
that tools could be implemented to convert the repository specific
metadata (and manifest file list) to the BagIt specification.

## BagIt datasets

<ul>
{% for dataset in site.data.bagit %}
{% assign datasetid = dataset[0] %}
{% assign meta = dataset[1].bag-info %}

{% assign pubdate = meta.Bagging-Date | split: '-' %}
{% assign pubdate = pubdate[0] %}

<li>
{{ meta.Contact-Name | join: "; " }} ({{ pubdate }}): <a href="landingpage/bagit/{{ datasetid }}">{{ meta.External-Description }}</a>. {{ meta.Source-Organization }}. (dataset).
</li>

{% endfor %}
</ul>

## Radboud datasets

<ul>
{% for dataset in site.data.radboud %}

{% assign datasetid = dataset[0] %}
{% assign meta = dataset[1].meta %}

{% assign datasetid = meta.CollectionIdentifier %}
{% assign authors = meta.Authors | join: "; " | default: "Unknown"  %}
{% assign pubdate = meta.PublicationDate | split: " " %}
{% assign pubdate = pubdate[0] | split: "-" %}
{% assign pubdate = pubdate[2] %}

{% if datasetid %}
<li>
{{ authors }} ({{ pubdate }}): <a href="landingpage/radboud/{{ datasetid }}">{{ meta.Title }}</a>. Version {{ meta.Version }}. {{ meta.Publisher }}. (dataset). {{ meta.PersistentURL }}
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
{{ authors }} ({{ pubdate }}): <a href="landingpage/zenodo/{{ datasetid }}">{{ meta['metadata']['title'] }}</a>. Version {{ meta.versions.index }}. Zenodo. (dataset). {{ meta.links.doi }}
</li>

{% endfor %}
</ul>

## OpenNeuro datasets

<ul>
{% for dataset in site.data.openneuro %}
{% assign meta = dataset[1] %}

{% assign authors = meta.author | join: "; " | default: "Unknown"  %}

<li>
{{ authors }} ({{ meta.year }}): <a href="landingpage/openneuro/{{ meta.id }}">{{ meta.title }}</a>. OpenNeuro. (dataset). https://doi.org/{{ meta.doi }}
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
{{ authors }} ({{ meta.publicationYear }}): <a href="landingpage/dataverse/{{ datasetid }}">{{ meta.titles.title }}</a>. DataverseNL. (dataset). https://doi.org/{{ doi }}
</li>

{% endfor %}
</ul>

## Yoda datasets

<ul>
{% for dataset in site.data.yoda %}
{% assign datasetid = dataset[0] %}
{% assign meta = dataset[1] %}

{% assign authors = '' %}
{% for creator in meta.Creator %}
{% assign authors = authors | append: '; ' | append: creator.Name.Given_Name | append: ' ' | append: creator.Name.Family_Name %}
{% endfor %}
{% for contributor in meta.Contributor %}
{% assign authors = authors | append: '; ' | append: contributor.Name.Given_Name | append: ' ' | append: contributor.Name.Family_Name %}
{% endfor %}
{% assign authors = authors | remove_first: "; " %}

{% assign pubdate = meta.Collected.End_Date | split: '-' %}
{% assign pubdate = pubdate[0] %}
  
<li>
{{ authors }} ({{ pubdate }}): <a href="landingpage/yoda/{{ datasetid }}">{{ meta.Title }}</a>. Version {{ meta.Version }}. University Utrecht. (dataset).
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
{{ authors }} ({{ meta.publicationYear }}): <a href="landingpage/4tu/{{ datasetid }}">{{ meta.titles.title }}</a>. 4TU.ResearchData. (dataset). https://doi.org/{{ doi }}
</li>

{% endfor %}
</ul>
