---
post_title: pg_config Executable Not Found
author: Luc
post_date: 2015-10-22 02:30:26
post_excerpt: ""
tags: postgres, python
categories: errors and problems
layout: post
permalink: >
  http://lucrussell.com/pg-config-executable-not-found-on-osx/
published: true
---
pg_config Executable Not Found
==============================
psycopg complains about missing pg_config executable. 

If you don't already have pg_config installed and on your path, do this
first:
 
     brew install postgresql 

Then install via psycopg2 on command line:

```
source venv/bin/activate
(venv)$ pip install psycopg2
...Successfully installed psycopg2-2.6.1
```