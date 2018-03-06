---
ID: 212
post_title: >
  Oracle Hangs on Stored Proc Call or
  Commit
author: Luc
post_date: 2013-03-27 08:56:58
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/oracle-hangs-on-stored-proc-call-or-commit/
published: true
---
## Problem
Error with Oracle hanging on a stored procedure call or commit statement.

## Solution
Does someone have an uncommitted session? SQL Developer will sometimes cause this (maybe a user doesn't have autocommit on?).

    select
    s.seconds_in_wait,
    s.blocking_instance,
    s.blocking_session,
    s.event,
    t.start_time,
    s.sid,
    s.serial#,
    s.username,
    s.status,
    s.schemaname,
    s.osuser,
    s.process,
    s.machine,
    s.terminal,
    s.program,
    s.module,
    to_char(s.logon_time,'DD/MON/YY HH24:MI:SS') logon_time
    from
    v$transaction t,
    gv$session s
    where
    s.saddr = t.ses_addr
    order by start_time;

Once you have a session id, use `Sql Developer Tools > Monitor Sessions` to see the problem SQL

See also [this link](http://stackoverflow.com/questions/10352300/use-gvsession-to-tell-if-a-query-is-hanging) on StackOverflow.