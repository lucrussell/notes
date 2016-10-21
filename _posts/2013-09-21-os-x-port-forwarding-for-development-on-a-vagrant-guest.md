---
ID: 512
post_title: >
  OS X Port Forwarding for Development on
  a Vagrant Guest
author: Luc
post_date: 2013-09-21 13:33:05
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/os-x-port-forwarding-for-development-on-a-vagrant-guest/
published: true
---
Temporarily repoint mydomain.com to localhost during development. This means you can develop mydomain.com, and when deploying to production you can be confident there are no 'localhost' references in your source. 

There are three elements to this:

<ol>
<li>
Edit your hosts file:
<code>sudo vi /etc/hosts</code>
Add the line:
    <code>192.168.50.1 mydomain.com</code>
(the IP address is the IP of the guest VM)
</li>    
<li>
Forward port 8080 on the host to the guest in your Vagrantfile:
<code>config.vm.network :forwarded_port, guest: 80, host: 8080, auto_correct: true</code>
</li>
<li>
Update iptables to forward requests to localhost:8080 to guest:

<code>sudo ipfw add 100 fwd 127.0.0.1,8080 tcp from any to any 80 in</code>
</li>
</ol>

Use <code>sudo ipfw flush</code> to remove the mapping.

Wrap it up in a function for your .functions file:

<pre class="lang:sh decode:true " title="Domain Forwarding Toggle Script" ># $1 Domain
# $2 IP Address
forward(){
	echo "$2 $1" | sudo tee -a /etc/hosts
	sudo ipfw add 100 fwd 127.0.0.1,8080 tcp from any to any 80 in
	dscacheutil -flushcache
}

# $1 Domain
remove_forward(){
	sudo sed -i "" "/$1/d" /etc/hosts
	dscacheutil -flushcache
	sudo ipfw flush
}</pre>