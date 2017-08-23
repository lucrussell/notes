---
post_title: sqlalchemy.exc.OperationalError
layout: post
published: true
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