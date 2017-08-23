---
ID: 689
post_title: sqlalchemy.exc.OperationalError
author: Luc
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/sqlalchemy-exc-operationalerror/
published: true
post_date: 2017-08-23 19:12:38
tags:
  - postgres
categories:
  - errors and problems
---
**Symptom**

I encountered this error while trying to run commands on Postgres running in a Docker container:

    sqlalchemy.exc.OperationalError: (psycopg2.OperationalError) FATAL:  could not write init file

**Solution**

Ensure Docker has enough disk space, see [Docker Quick Reference](http://lucrussell.com/docker-quick-reference).