---
ID: 386
post_title: 'Can&#8217;t see JBoss from Another Machine'
author: Luc
post_date: 2013-05-30 07:51:58
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/cant-see-jboss-from-another-machine/
published: true
---
You need to set the bind address(es) to allow others to see the server. E.g. on Windows:
<code>run.bat -b 0.0.0.0</code>