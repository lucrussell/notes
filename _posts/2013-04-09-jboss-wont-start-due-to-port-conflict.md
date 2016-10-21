---
ID: 243
post_title: 'JBoss Won&#8217;t Start Due to Port Conflict'
author: Luc
post_date: 2013-04-09 15:58:07
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/jboss-wont-start-due-to-port-conflict/
published: true
---
<ul>
	<li>Do a find/replace for the port: <code>netstat -ano | grep </code></li>
	<li>Take the pid and look in Windows Task Manager, add the pid column in Options if necessary</li>
	<li>Kill the process, or change it in the config like this:</li>
</ul>
<code>
cd /PATH/jboss/local
grep "badport" . -rl
</code>
<ul>
	<li>Or just try a restart, that will sometimes fix it</li>
</ul>