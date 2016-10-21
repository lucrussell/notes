---
ID: 591
post_title: 'Grails Error: Fatal Error During Compilation (Groovy Grails Tool Suite)'
author: Luc
post_date: 2015-07-22 02:24:49
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/grails-error-fatal-error-during-compilation-groovy-grails-tool-suite/
published: true
en_guid:
  - 90497122-06e5-40f4-a1b2-2e85c1766a30
en_modified:
  - "1437574852000"
---
<p><code>Fatal error during compilation org.springframework.beans.factory.BeanDefinitionStoreException: Failed to read candidate component class: URL [jar:file:/Users/lrussell/.grails/ivy-cache/org.grails/grails-hibernate/jars/grails-hibernate-2.2.4.jar!/org/codehaus/groovy/grails/compiler/gorm/GormTransformer.class]; nested exception is java.lang.NoClassDefFoundError: org/springframework/core/type/classreading/AnnotationMetadataReadingVisitor</code></p>

<p>First tried removing ~/.grails/</p>

<p>And then running the grails RunApp again. It downloaded the cache fresh, might take a while. Didn't seem to make any difference though...</p>

<p>Then in the Groovy Grails Tools Suite, I went to the Grails Plugin Manager (right click project &gt; Grails Tools &gt; Grails Plugin Manager), showed all plugins currently installed. Some required an update, so updated everything. That worked :)</p>