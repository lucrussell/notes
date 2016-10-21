---
ID: 339
post_title: 'Error while loading shared libraries: libXau.so.6'
author: Luc
post_date: 2013-04-26 07:48:55
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/error-while-loading-shared-libraries-libxau-so-6/
published: true
---
<code>/usr/bin/php: error while loading shared libraries: libXau.so.6: failed to map segment from shared object: Cannot allocate memory</code>
 
Caused by: Did you try to update memory settings in php config? Seems if you do this, you also need to increase the amount available to Apache, i.e.

<code>vi /usr/local/apache/conf/httpd.conf</code>

And set the RLimitMEM to something like 651048618

See this <a href="http://serverfault.com/questions/403369/getting-internal-server-error-after-updating-server-config-via-whm" title="stackoverflow.com">reference</a>.