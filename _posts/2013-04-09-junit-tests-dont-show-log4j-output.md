---
ID: 227
post_title: 'JUnit Tests Don&#8217;t Show log4j Output'
author: Luc
post_date: 2013-04-09 15:58:07
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/junit-tests-dont-show-log4j-output/
published: true
---
Add this to the VM arguments in the run configuration: 
<code>-Dlog4j.configuration=file:/C:/PATH/log4j.xml</code>