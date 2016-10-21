---
ID: 248
post_title: >
  Could not initialize class
  net.sf.cglib.proxy.Enhancer
author: Luc
post_date: 2013-04-09 15:58:07
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/could-not-initialize-class-net-sf-cglib-proxy-enhancer/
published: true
---
Nested exception is java.lang.NoClassDefFoundError: Could not initialize class net.sf.cglib.proxy.Enhancer.
<ul>

	<li> Increase Spring logging to debug in log4j.xml</li>

	<li> The issue starts with java.lang.NoClassDefFoundError: org/objectweb/asm/Type</li>

	<li> This is maybe due to a class conflict: Type has moved in newer version of Spring. Remove old cglib from classpath and ensure the asm.jar in use is the latest</li>

</ul>