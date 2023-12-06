# BagIt Research Data (BIRD)

This is a toy project inspired by the
[BagIt](https://en.wikipedia.org/wiki/BagIt) standard for storage
and network transfer of arbitrary digital content, among others
research data.

I figured that if all research datasets were represented as "Bags"
with metadata, and with pointers to the actual data on a download
server using the `fetch.txt` file, writing a repository server might
be rather simple. This project is an exploration in writing such a
research data repository server.

## Metadata

The web server implemented in this project hosts the metadata of
research data collections (or "datasets"). It consists of an overview
page that lists all datasets, and an individual langing page for
each dataset.

## Data

The landing page contains (or should contain) links to the actual
data files to download, but the files themselves are not hosted on
the same server. Instead they could be on a FTP server, a WEBDAV
server, or an S3 server.

## Dataset creation

At this moment there is no mechanism implemented or procedure
documented regarding the construction of datasets. Also the minting
of DOIs is not part of the current efforts. It is assumed that
somehow a (JSON, YAML, TSV, CSV, or XML) file with metadata is
provided, and that the actual files have been made available on a
download server.

## Running this website

This project is implemented using [Jekyll](http://jekyllrb.com/),
a static website generator. To run it on your own computer, you
should install Ruby and Gem, and run

    gem install bundler jekyll

    git clone https://github.com/robertoostenveld/bird.git
    cd bird
    bundle install

Subsequently, you can convert the markdown into html documents with

    bundle exec jekyll serve --livereload

