# BagIt Research Data (BIRD) repository

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

## Existing datasets and repositories

The project demonstrates a research data repository by reusing
some public datasets from the following research data repositories:

- <https://data.ru.nl>
- <https://zenodo.org>
- <https://openneuro.org>
- <https://dataverse.nl>
- <https://4tu.ru.nl>

## Metadata

The web server implemented in this project hosts the metadata of
the datasets (or "research data collections"). It consists of an
overview page that lists all datasets, and an individual landing
page for each dataset.

If this were a proper repository publishing the original datasets,
then the DOI of the datasets shoudl directo to the corresponding
landing page here.

## Data

Besides the metadata, the landing page contains (or should contain)
links to the actual data files to download. The files themselves
are not hosted on the same web server but could be on a FTP server,
a WEBDAV server, an S3 server, etc.

## Dataset creation

At this moment there is no mechanism implemented nor procedure
documented regarding the construction of datasets. Also the minting
of DOIs is not part of the current efforts. It is assumed that
a file with metadata is provided in JSON, YAML, TSV, CSV, or XML
format, and that the actual files have been made available on a
download server.

## Deploying this website

This project is implemented using [Jekyll](http://jekyllrb.com/),
a static website generator. To run it on your own computer, you
should install Ruby and Gem, and run

    gem install bundler jekyll

    git clone https://github.com/robertoostenveld/bird.git
    cd bird
    bundle install

Subsequently, you can convert the markdown into html documents with

    bundle exec jekyll serve --livereload  --incremental

Since I am also running this site on Github pages, you may need to
edit the `baseurl` field in the `_config.yml` file. For a local
deployment it should be empty (`""`), for deployment on Github
it should correspond to the repository name (`"bird"`) .
