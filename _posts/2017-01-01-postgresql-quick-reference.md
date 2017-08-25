---
ID: 696
post_title: PostgreSQL Quick Reference
author: Luc
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/postgresql-quick-reference/
published: true
post_date: 2017-01-01 19:40:44
tags:
  - postgres
categories:
  - postgres
---
## Connect

    $ psql -h localhost -d mydb -U myuser

## List Databases
From within a psql session:

    l

## List Tables

    dt

## Connect To DB

    c myuser

## Execute SQL in a File

    $ psql -U myuser -d mydb -a -f myfile.sql

## Run a Query

    $ psql -U myuser -d mydb -c 'SELECT * FROM my_table'

## Output to File
Example shows opening a file, listing tables to the file, and finally closing the file:

    db=>o out.txt
    db=>dt
    db=>q

## Get PostgreSQL Logs
    
    db=> show log_destination;

See [this reference](http://blog.endpoint.com/2014/11/dear-postgresql-where-are-my-logs.html).

## Check Running Queries

    SELECT pid, age(query_start, clock_timestamp()), usename, query 
    FROM pg_stat_activity 
    WHERE  query NOT ILIKE '%pg_stat_activity%' 
    ORDER BY query_start desc;

See also [this reference](https://russ.garrett.co.uk/2015/10/02/postgres-monitoring-cheatsheet/).

## Terminate a Running Query

    select pg_terminate_backend(pid int)

## Check Locks
See [this reference](https://wiki.postgresql.org/wiki/Lock_Monitoring). 

## Do Something for Every Child Table

    DO
    $$
    DECLARE
        row record;
    BEGIN
        FOR row IN select c.relname as tablename from pg_inherits JOIN pg_class AS c ON (inhrelid=c.oid) JOIN pg_class AS p ON (inhparent=p.oid) WHERE p.relname = 'my_table'
        LOOP
            EXECUTE 'drop TABLE ' || quote_ident(row.tablename);
        END LOOP;
    END;
    $$;

## Insert Sample Data with Incrementing Values

    insert into my_table (name, thing, id)
    select 'user1', 'test' || x.id, 1
        from generate_series(40, 100, 1) as x(id);

Check the [generate_series](https://www.postgresql.org/docs/9.1/static/functions-srf.html) documentation for what the parameters mean.

## Convert a String to a Timestamp

    to_timestamp('2015-04-30 23:59:59', 'YYYY-MM-DD HH24:MI:SS')

## Partitioning
Refer to [this example](https://blog.engineyard.com/2013/scaling-postgresql-performance-table-partitioning) for how to partition tables for performance.