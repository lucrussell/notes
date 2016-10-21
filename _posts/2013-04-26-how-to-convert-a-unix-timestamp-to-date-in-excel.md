---
ID: 328
post_title: >
  How To Convert a Unix Timestamp to Date
  in Excel
author: Luc
post_date: 2013-04-26 07:36:28
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/how-to-convert-a-unix-timestamp-to-date-in-excel/
published: true
---

Use this formula: <code>=(A1/86400)+25569+(-5/24)</code>
(replace the 5 with the timezone offset)
See <a href="http://spreadsheetpage.com/index.php/tip/converting_unix_timestamps/" title="spreadsheetpage.com">here</a> for more info.