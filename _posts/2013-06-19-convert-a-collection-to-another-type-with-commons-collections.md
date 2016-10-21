---
ID: 453
post_title: >
  Convert a Collection to Another Type
  With Commons Collections
author: Luc
post_date: 2013-06-19 08:12:57
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/convert-a-collection-to-another-type-with-commons-collections/
published: true
---
 
<pre class="lang:java decode:true " title="Convert a Collection of one Type to Another Type with Commons Collections" >private Collection&lt;Apple&gt; convert(final Collection&lt;Orange&gt; values) {
    final Collection&lt;Apple&gt; converted = CollectionUtils.collect(values, new Transformer(){
      public Object transform(final Object target){
        Orange result = null;
        if(target != null){
            result = new Apple(target.getName());
        }
        return result;
      }
    });
    return converted;
}</pre>