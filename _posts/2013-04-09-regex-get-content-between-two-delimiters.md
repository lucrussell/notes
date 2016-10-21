---
ID: 206
post_title: 'Regex: Get Content Between Two Delimiters'
author: Luc
post_date: 2013-04-09 15:58:07
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/regex-get-content-between-two-delimiters/
published: true
---
 Non-greedy
<pre class="lang:java decode:true " >
//E.g. blahblah [GBP 200.0000] blahblah 
private String getValues(String values) {
    String patternStr = "\\[(.+?)\\]";
    Pattern pattern = Pattern.compile(patternStr);
    Matcher matcher = pattern.matcher(values);
    boolean matchFound = matcher.find();
    String groupStr = null;
    if (matchFound) {
        groupStr = matcher.group(0);
    }
    return groupStr;
    //Returns [GBP 200.0000]
}
</pre>