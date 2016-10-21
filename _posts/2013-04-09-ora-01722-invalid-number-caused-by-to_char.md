---
ID: 269
post_title: 'ORA-01722: Invalid Number Caused by to_char'
author: Luc
post_date: 2013-04-09 15:58:06
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/ora-01722-invalid-number-caused-by-to_char/
published: true
---
<ul>

	<li>This might be caused by running to_char on a timestamp like this: to_char(dp.calc_date, 'dd/Mon/yyyy hh:mi:s').</li>

	<li>Try just returning the date without trying to convert it first.</li>

	<li>More about this error <a href="http://asktom.oracle.com/pls/asktom/f?p=100:11:0::::P11_QUESTION_ID:45012348053" title="asktom link">here</a>.</li>


</ul>