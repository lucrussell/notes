---
ID: 219
post_title: 'Eclipse/SVN: ClientException: system cannot find the file specified'
author: Luc
post_date: 2013-04-09 15:58:07
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/eclipsesvn-clientexception-system-cannot-find-the-file-specified/
published: true
---
Message: <code>svn: Can't create tunnel: The system cannot find the file specified.<code>
<ul>
	<li>Check the SVN Interface in Eclipse/Preferences - try SVNKit instead of JavaHL</li>


	<li>This error also manifests as <code>malformed reply from SOCKS server</code></li>
</ul>