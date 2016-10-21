---
ID: 599
post_title: >
  DBUnit TypeCastException Unable to
  typecast value 0 of type
  java.lang.String to TIMESTAMP
author: Luc
post_date: 2015-07-22 14:38:10
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/dbunit-typecastexception-unable-to-typecast-value-0-of-type-java-lang-string-to-timestamp/
published: true
en_guid:
  - 458f0705-52ee-4c86-b719-bf2a5c33e310
en_modified:
  - "1437576569000"
---
<p>But the column isn't a timestamp anyway, so not sure why DBUnit wants to treat it as such.</p>

<p><b>Solution</b></p>

<p>Set columnSensing to false when creating the dataset. For a FlatXmlDataSet, you can specify a boolean in the constructor to achieve this.</p>