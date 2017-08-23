---
author: Luc
layout: post
published: true
tags:
  - postgres
categories:
  - errors and problems
---
## sqlalchemy.exc.OperationalError
**Symptom**

While trying to run commands on Postgres running in a Docker container:

    sqlalchemy.exc.OperationalError: (psycopg2.OperationalError) FATAL:  could not write init file

**Solution**

Ensure docker has enough disk space, see [Docker Quick Reference](http://lucrussell.com/docker-quick-reference).