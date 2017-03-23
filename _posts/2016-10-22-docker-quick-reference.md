---
ID: 614
post_title: Docker Quick Reference
author: Luc
post_date: 2016-10-22 02:30:26
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/docker-quick-reference/
published: true
tags:
  - docker
category:
  - 'a:1:{i:0;s:15:"quick reference";}'
categories:
  - quick reference
tags_input:
  - 'a:1:{i:0;s:86:"a:4:{i:0;s:21:"wpghs_pre_import_args";i:1;s:4:"tags";i:2;s:5:"hello";i:3;s:5:"world";}";}'
---
<h1>Table of Contents</h1>

<ul>
<li><a href="#docker-compose-force-rebuild">Docker Compose Force Rebuild</a></li>
<li><a href="#working-with-docker-for-mac">Working With Docker for Mac</a> 

<ul>
<li><a href="#aliasing-0000-to-work-around-dynamic-ips">Aliasing 0.0.0.0 to work around dynamic IPs</a></li>
<li><a href="#accessing-the-xyve-virtual-machine">Accessing The Xyve Virtual Machine</a></li>
<li><a href="#add-an-internal-company-registry-or-repo">Add an Internal Company Registry or Repo</a></li>
</ul></li>
<li><a href="#get-into-a-docker-container-without-docker-enter">Get Into a Docker Container without docker-enter</a></li>
<li><a href="#get-into-a-docker-image-which-fails-to-start">Get Into a Docker Image which Fails to Start</a></li>
<li><a href="#free-up-disk-space-used-by-docker">Free up Disk Space Used by Docker</a></li>
<li><a href="#temporarily-install-a-package-for-troubleshooting">Temporarily Install a Package for Troubleshooting</a></li>
<li><a href="#run-a-container-with-env-variables-for-testing">Run A Container With Env Variables for Testing</a></li>
<li><a href="#remove-containers-created-and-exited-2-weeks-ago">Remove Containers Created and Exited 2 Weeks ago</a></li>
<li><a href="#remove-all-exited-containers">Remove All Exited Containers</a></li>
<li><a href="#grep-docker-stdout-and-stderr">Grep Docker stdout and stderr</a></li>
<li><a href="#keep-a-container-running">Keep a Container Running</a></li>
<li><a href="#run-a-container-with-a-link-to-another">Run A Container With a Link to Another</a></li>
<li><a href="#logs">Logs</a></li>
<li><a href="#other-references">Other References</a></li>
</ul>

<h2>Docker Compose Force Rebuild</h2>

Also see <a href="http://stackoverflow.com/questions/32612650/how-to-get-docker-compose-to-always-start-fresh-images">here</a>.

<pre><code>docker-compose rm -v -f
docker-compose build --no-cache
docker-compose up --force-recreate
</code></pre>

<h2>Working With Docker for Mac</h2>

<h3>Aliasing 0.0.0.0 to work around dynamic IPs</h3>

To solve this problem:

<blockquote>
  I want to connect from a container to a service on the host. The 
  mac has a changing IP address or no address if you have no network access
</blockquote>

The current recommendation is to attach an unused IP to the lo0 interface on the Mac e.g.

<pre><code>sudo ifconfig lo0 alias 10.200.10.1/24
</code></pre>

Make sure your service is listening on this address or 0.0.0.0 
(i.e. not 127.0.0.1). Then any containers which need to access the 
service can use the <code>10.200.10.1</code> address.

<h3>Accessing The Xyve Virtual Machine</h3>

You might need to do this after restarting/upgrading docker. To get into the xyve vm use <code>screen</code>:

<pre><code>screen ~/Library/Containers/com.docker.docker/Data/com.docker.driver.amd64-linux/tty 
</code></pre>

The login is 'root', no password.

<h3>Add an Internal Company Registry or Repo</h3>

<pre><code>vi /etc/hosts 
</code></pre>

and add the address e.g.:

<pre><code>10.10.10.100   my-registry.mycompany.com
</code></pre>

Exit screen with <code>Ctrl-a</code> then <code>k</code>.

Here is a <code>screen</code> reference: http://ss64.com/osx/screen.html.

<h2>Get Into a Docker Container without docker-enter</h2>

<pre><code>docker exec -it 963ffd75c1b5 /bin/bash
</code></pre>

<h2>Get Into a Docker Image which Fails to Start</h2>

<pre><code>docker run -it applications_mycontainer /bin/bash 
</code></pre>

Use <code>docker images</code> to find the correct image name

<h2>Free up Disk Space Used by Docker</h2>

See <a href="http://blog.yohanliyanage.com/2015/05/docker-clean-up-after-yourself/">this reference</a>.

<h2>Temporarily Install a Package for Troubleshooting</h2>

If you need to, you can probably simply install packages in any transient container, e.g.:

<pre><code>apt-get update
apt-get install netcat
nc -v -w3 10.10.10.100 5432
</code></pre>

<h2>Run A Container With Env Variables for Testing</h2>

<pre><code>docker run -it -e  MY_ENV_VAR=somevalue myrepo/myapp:latest /bin/bash
</code></pre>

<h2>Remove Containers Created and Exited 2 Weeks ago</h2>

<pre><code>docker ps -a | grep "2 weeks" | grep "Exited" | awk '{print $1}' | sudo xargs docker rm
</code></pre>

<h2>Remove All Exited Containers</h2>

<pre><code>docker ps -a | grep Exit | awk '{print $1}' |  xargs docker rm
</code></pre>

<h2>Grep Docker stdout and stderr</h2>

E.g. if you have an application that's writing to both streams and you're not sure where logs are going:

<pre><code>docker logs 4017b8a68f98 2&gt;&amp;1 | grep
</code></pre>

<h2>Keep a Container Running</h2>

E.g. if it starts and immediately exits:

<pre><code>sudo docker run -t -i my-registry/mycontainer /bin/bash
</code></pre>

This will attach you directly to the container so you can check the logs.

<pre><code>sudo docker run -d my-registry/my-container /bin/bash
</code></pre>

This will start it detached.

<h2>Run A Container With a Link to Another</h2>

<pre><code>docker run --rm -t -i --name mycontainer --link docker_consul_1 my-registry/mycontainer
</code></pre>

<h2>Logs</h2>

Get the last 20 lines of logs:

<pre><code>docker logs --tail 20 fc805ce579d3
</code></pre>

<h2>Other References</h2>

<a href="https://github.com/wsargent/docker-cheat-sheet">Cheat sheet</a>.

[wpghs target='view' type='link' text='View and edit this post on GitHub']