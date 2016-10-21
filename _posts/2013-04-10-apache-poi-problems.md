---
ID: 303
post_title: Apache POI Problems
author: Luc
post_date: 2013-04-10 16:18:07
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/apache-poi-problems/
published: true
---
POI doesn't like:
<ul>

 	<li>Autofilter on column headings</li>

 	<li>When using <code>InputStream inp = this.getClass().getResourceAsStream("myfile.xls");</code>, you need to refresh the file in Eclipse before running tests - otherwise it uses a cached copy of the file</li>

</ul>