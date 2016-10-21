---
ID: 474
post_title: How to Change the Default SSH Port
author: Luc
post_date: 2013-07-04 09:46:47
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/how-to-change-the-default-ssh-port/
published: true
---
First follow this reference: <a href="http://wiki.centos.org/HowTos/Network/SecuringSSH" title="Securing SSH">http://wiki.centos.org/HowTos/Network/SecuringSSH</a>

However, if it doesn't work you might also need to update iptables:
<code>
iptables -I INPUT -m state --state NEW -p tcp --dport <strong>NEW_PORT</strong> -j ACCEPT
iptables -I INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
/etc/init.d/iptables save
service sshd stop
service sshd start
</code>