---
ID: 447
post_title: >
  How To Select Elements From a Collection
  With Apache Commons Collections
author: Luc
post_date: 2013-06-18 07:53:11
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/select-elements-from-a-collection-with-apache-commons-collections/
published: true
---
 
<pre class="lang:java decode:true " title="Code Snippet: Select Elements from a Collection with Apache Commons Collections" >private List&lt;Vegetable&gt; getVegetablesLike(List&lt;Vegetable&gt; allVegetables, 
                final Vegetable vegetable) {
    return (List&lt;Vegetable&gt;) 
        select(allVegetables, new Predicate() {
        @Override
        public boolean evaluate(Object o) {
            Vegetable other = (Vegetable) o;
            return other.equals(vegetable);
        }
    });
}</pre>