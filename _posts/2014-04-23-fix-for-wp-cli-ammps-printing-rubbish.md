---
ID: 526
post_title: Fix for WP CLI on AMMPS Printing Rubbish
author: Luc
post_date: 2014-04-23 20:01:12
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/fix-for-wp-cli-ammps-printing-rubbish/
published: true
---
Environment: <code>OSX, AMMPS</code>

Maybe caused by the particular version of PHP shipped with AMMPS and symlinked by default (PHP 5.3.21 at this time).

For example this command:
 
<code> /Applications/AMPPS/php/bin/php ~/wp-cli.phar --info </code>
Prints: 

<code>???p?</code>

To fix it, update AMMPS to the latest. This includes PHP 5.4.11, but does not link it as the default.

Now this command:
<code>/Applications/AMPPS/php-5.4/bin/php ~/wp-cli.phar --info
</code>

Prints:

<code>PHP binary:	/Applications/AMPPS/php-5.4/bin/php-5.4.11
PHP version:	5.4.11
php.ini used:	
WP-CLI root dir:	phar://wp-cli.phar
WP-CLI global config:	
WP-CLI project config:	
WP-CLI version:	0.15.0</code>

Now fix it more permanently by adding that version to your PATH, i.e.

<code>export PATH="/Applications/AMPPS/php-5.4/bin/:/Applications/AMPPS/mysql/bin:$PATH"</code>