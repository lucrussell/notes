---
ID: 224
post_title: getTextContext undefined for type Node
author: Luc
post_date: 2013-04-09 15:58:07
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/gettextcontext-undefined-for-type-node/
published: true
---
This is a classpath ordering issue. The jdk lib needs to be referenced before the xml-apis.jar as well as the xmlParserAPIs.jar. Edit the project properties in Eclipse and move the jdk lib up.