---
ID: 347
post_title: DocuWiki Strict Standards error
author: Luc
post_date: 2013-04-27 13:11:22
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/docuwiki-strict-standards-error/
published: true
---
DocuWiki prints out lots of warning information like "Strict Standards: Declaration of ..."

Solution 1: You may be able to set this in .htaccess, however some hosts may not respect the setting in .htaccess
See <a href="http://perishablepress.com/advanced-php-error-handling-via-htaccess/" title="perishablepress.com">this reference</a>.

Solution 2: Reduce the error reporting in php.ini e.g. "error_reporting = E_ALL & ~E_NOTICE"
See <a href="http://stackoverflow.com/questions/9983286/disabling-strict-standards-in-php-5-4" title="stackoverflow.com">here</a>.