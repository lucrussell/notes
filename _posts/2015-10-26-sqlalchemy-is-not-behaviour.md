---
ID: 646
post_title: 'SQLAlchemy &#8220;is not&#8221; behaviour'
author: Luc
post_date: 2015-10-26 01:20:42
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/sqlalchemy-is-not-behaviour/
published: true
tags_input:
  - 'a:4:{i:0;s:21:"wpghs_pre_import_args";i:1;s:4:"tags";i:2;s:5:"hello";i:3;s:5:"world";}'
tags:
  - python
categories:
  - errors and problems
---
If you want to use `!=` but lint complains, use `isnot` instead. See [this reference][1] for more details.

 [1]: http://docs.sqlalchemy.org/en/rel_1_0/orm/tutorial.html