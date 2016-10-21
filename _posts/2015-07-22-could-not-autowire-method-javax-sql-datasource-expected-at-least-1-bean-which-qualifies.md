---
ID: 593
post_title: 'Could not autowire method&#8230; javax.sql.DataSource: expected at least 1 bean which qualifies&#8230;'
author: Luc
post_date: 2015-07-22 13:34:06
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/could-not-autowire-method-javax-sql-datasource-expected-at-least-1-bean-which-qualifies/
published: true
en_guid:
  - 3b8b99d0-b9ae-4a67-b5a1-3d24c98af975
en_modified:
  - "1437572053000"
---
<p>If you are extending AbstractTransactionalJUnit4SpringContextTests, are you sure you need to do that? Removing that might fix it.</p>