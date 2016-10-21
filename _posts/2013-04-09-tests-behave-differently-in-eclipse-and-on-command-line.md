---
ID: 261
post_title: >
  Tests Behave Differently in Eclipse and
  on Command Line
author: Luc
post_date: 2013-04-09 15:58:06
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/tests-behave-differently-in-eclipse-and-on-command-line/
published: true
---
They might behave differently because they usually run together when running on command line, and individually in Eclipse.  
If using Spring, you need to use <code>@DirtiesContext</code> to rebuild the Spring context if one class has dirtied it, e.g. by setting up a mock object which then affects a later running test.