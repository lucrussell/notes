---
ID: 258
post_title: >
  Unable to Pass Variables from Java to a
  Stored Proc
author: Luc
post_date: 2013-04-09 15:58:06
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/unable-to-pass-variables-from-java-to-a-stored-proc/
published: true
---
Problem: You are passing info to the db, but the proc doesn't appear to receive it.  The stored proc works fine when executed directly from Toad or SQL Developer.  

This might be due to a missing i18n library which should be on your runtime classpath.