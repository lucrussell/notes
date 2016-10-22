---
ID: 620
post_title: pg_config Executable Not Found
author: Luc
post_date: 2015-10-21 12:40:56
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/pg_config-executable-not-found/
published: true
tags: [python, postgres]
categories:
  - errors and problems
---

psycopg complains about missing pg_config executable.

If you don't already have pg_config installed and on your path, do this first:

     brew install postgresql 
    

Then install psycopg2 on command line:

    source venv/bin/activate
    (venv)$ pip install psycopg2
    ...Successfully installed psycopg2-2.6.1

