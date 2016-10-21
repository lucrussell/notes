---
ID: 238
post_title: >
  How to Set Up SQL Debugging With SQL
  Developer
author: Luc
post_date: 2013-04-09 15:58:07
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/how-to-set-up-sql-debugging-with-sql-developer/
published: true
---
<ul>

<li>Request the "DEBUG ANY PROCEDURE" privilege from your DBAs.  This allows full interactive debugging of stored procs and functions in SQL Developer (probably Toad as well).</li>
<li>In Tools/Preferences/Debugger, set 'Prompt for Debugger...' (use own ip address when prompted)</li>
<li>Open the body of a package to add a breakpoint</li>
<li>Then compile for debug</li>

<li>Right click somewhere in the package and click debug</li>

<li>Doesn't work from an external app (have to run the proc from inside sql developer)  </li>

	<li>See this <a href="http://sueharper.blogspot.com/2006/07/remote-debugging-with-sql-developer_13.html" title="Remote Debugging How To">Remote Debugging How To</a> for more details</li>

</ul>