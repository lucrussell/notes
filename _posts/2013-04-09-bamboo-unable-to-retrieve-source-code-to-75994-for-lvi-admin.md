---
ID: 234
post_title: 'Bamboo: Unable to retrieve source code to &#8216;75994&#8217; for &#8216;LVI-ADMIN&#8217;'
author: Luc
post_date: 2013-04-09 15:58:07
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/bamboo-unable-to-retrieve-source-code-to-75994-for-lvi-admin/
published: true
---
## Problem
Bamboo error message: unable to retrieve source code to &#8216;75994&#8217; for &#8216;LVI-ADMIN&#8217;
 
## Solution
Configure the plan to perform a clean checkout, see [this Bamboo issue](http://confluence.atlassian.com/display/BAMKB/SVN+update+fails+with+NullpointerException). It's not exactly the same, but a similar issue.