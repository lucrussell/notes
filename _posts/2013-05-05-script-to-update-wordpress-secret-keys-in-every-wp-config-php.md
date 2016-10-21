---
ID: 371
post_title: >
  Script to Update WordPress Secret Keys
  in Every wp-config.php
author: Luc
post_date: 2013-05-05 21:16:10
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/script-to-update-wordpress-secret-keys-in-every-wp-config-php/
published: true
---
<pre class="lang:sh decode:true " title="Script to Update WordPress Secret Keys" >#!/bin/bash
find . -name wp-config.php -print | while read line
do 
	curl http://api.wordpress.org/secret-key/1.1/salt/ &gt; wp_keys.txt
	sed -i.bak -e '/put your unique phrase here/d' -e '/AUTH_KEY/d' -e '/SECURE_AUTH_KEY/d' -e '/LOGGED_IN_KEY/d' -e '/NONCE_KEY/d' -e '/AUTH_SALT/d' -e '/SECURE_AUTH_SALT/d' -e '/LOGGED_IN_SALT/d' -e '/NONCE_SALT/d' $line
	cat wp_keys.txt &gt;&gt; $line
	rm wp_keys.txt
done</pre>