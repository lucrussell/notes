---
ID: 566
post_title: Java Collections Quick Reference
author: Luc
post_date: 2015-03-21 18:38:02
post_excerpt: >
  A cheat sheet for my frequently
  used/forgotten Java Collections
  snippets.
layout: post
permalink: >
  http://lucrussell.com/java-collections-quick-reference/
published: true
---
A cheat sheet for my frequently used/forgotten Java Collections snippets.
<h3>Quickly Create a List</h3>
<pre class="lang:java decode:true ">import static java.util.Arrays.asList;
asList("hello", "goodbye");
import static java.util.Collections.unmodifiableList;
unmodifiableList(asList("hello", "goodbye"));
</pre>
<h3>Empty Collection Syntax</h3>
<pre class="lang:java decode:true ">List&lt;String&gt; requiredInputs = Collections.&lt;String&gt;emptyList();
</pre>
Also see <a title="StackOverflow" href="http://stackoverflow.com/questions/5552258/collections-emptylist-vs-new-instance" target="_blank">here</a>.
<h3>Safe Empty Array</h3>
<pre class="lang:java decode:true ">public static String[] safe(String[] other ) {
    return other == null ? new String[0] : other;
}</pre>
<h3>Convert Array to List</h3>
<pre class="lang:java decode:true ">Arrays.asList(values)
</pre>
<h3>Collection to Array</h3>
<pre class="lang:java decode:true ">values.toArray(new String[values.size()])
</pre>
<h3>Loop Over Keys And Values In A Map</h3>
<pre class="lang:java decode:true ">for (Iterator&lt;Map.Entry&lt;String, Object&gt;&gt; it = resultsData.entrySet().iterator(); it.hasNext();) {
            Map.Entry&lt;String, Object&gt; entry = it.next();
            String key = entry.getKey();
            Object value = entry.getValue();
            System.out.println(String.format("key: %s, value: %s", key, value));
        }</pre>