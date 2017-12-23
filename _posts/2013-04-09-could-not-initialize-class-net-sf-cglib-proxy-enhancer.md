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

## Problem
The error message was:

    Could not initialize class net.sf.cglib.proxy.Enhancer

The nested exception leading up to this was:

    java.lang.NoClassDefFoundError: Could not initialize class net.sf.cglib.proxy.Enhancer

## Solution

* Increase Spring logging to debug in log4j.xml.
* The issue initially began with `java.lang.NoClassDefFoundError: org/objectweb/asm/Type`.
* The problem could be due to a class conflict: the `Type` class has moved in newer version of Spring. Try removing the old `cglib` from the classpath and ensure the asm.jar in use is the latest one.