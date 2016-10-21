---
ID: 378
post_title: 'JBoss: JDWP No transports initialized'
author: Luc
post_date: 2013-05-20 15:21:34
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/jboss-jdwp-no-transports-initialized/
published: true
---
My java opts was like this:
<code>set JAVA_OPTS=-Xdebug -Xrunjdwp:transport=dt_socket,address=8787,server=n,suspend=n %JAVA_OPTS%</code>

Changed it to this instead:
<code>set JAVA_OPTS=-agentlib:jdwp=transport=dt_socket,address=8787,server=y,suspend=n %JAVA_OPTS%</code>