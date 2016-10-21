---
ID: 467
post_title: >
  How to Set Up Clustered DNS With cPanel
  DNSONLY
author: Luc
post_date: 2013-07-05 15:10:48
post_excerpt: >
  Steps for setting up a clustered DNS
  with the cPanel DNSONLY product.
layout: post
permalink: >
  http://lucrussell.com/how-to-set-up-clustered-dns-with-cpanel-dns-only/
published: true
---
<h2>Why</h2>
<ul>
<li>If you rely on a DNS service running on your web server, every query must go to this server, meaning the queries will be slower for geographically remote users.
</li>
<li>Outages on your web server will affect DNS resolution which is used for other functions, e.g email delivery. If your web server and DNS are hosted together, and your web server goes down for a few minutes, mail to that domain will be returned to the sending server's queue and marked as a permanent failure. If the DNS service is clustered on separate servers, even if your web server goes down for a few minutes, the DNS server will still be running.
</li>
<li>You could use a 3rd party DNS service like <a href="http://dnsmadeeasy.com" title="DNS Made Easy">DNS Made Easy</a>. However, you'll have to manually update this 3rd party service each time you want to modify account details. cPanel will manage this for you by synchronising changes out to DNSONLY servers.</li>
</ul>

<h2>Steps</h2>
These steps apply if you have an existing cPanel WHM web server, and you want to create a DNS cluster, adding a new cPanel DNSOnly server.
<ol>
<li>Obtain a new server, a hardware spec of 256mb memory, 10/15GB disk should be sufficient. <a href="http://www.lowendtalk.com/categories/offers" title="Low End Talk">Low End Talk</a> sometimes have offers for this sort of server</li>
<li>Install pre-requisites if necessary. On a fresh Centos 6.4 install, I needed:</li>
<blockquote>
<code>yum install wget
yum install perl</code>
</blockquote>
<li>Install cPanel DNSOnly:</li>
<blockquote>
<code>cd /home
wget -N http://httpupdate.cpanel.net/latest-dnsonly
sh latest-dnsonly</code>
</blockquote>
<li>Go to https://your_ip:2087/ and follow the wizard</li>
<li>On your existing cPanel WHM server (the original web server):</li>
<ul>
<li>Add your new server under clustering, set it to sync</li>
<li>Now follow <a href="http://www.docs.cpanel.net/twiki/bin/view/AllDocumentation/WHMDocs/ConfigureCluster" title="cPanel Documentation">these steps</a> from the cPanel documentation</li>
<li>Set the server you're adding to Synchronize Changes</li>
<li>Go to Edit DNS Zone and add a new NS record, pointing to the IP of the new DNS server</li>
</ul>
<li>On the new DNS server:</li>
<ul>
<li>Go to WHM > Configure Cluster, check that the main server appears and the DNS role is Standalone. Generally it is not recommended setting up the DNS server to synchronize data to a web server</li>
</ul>
</ol>

<h2>Check the Setup</h2>
<ol>
<li>Log in to WHM on the main server and Synchronize one zone to all servers, with a test domain</li>
<li>ssh into the dnsonly server, <code>ls /var/named/*.com.db</code> and you should see the synchronised account has been sent over</li>
<li>You should also see the new zone on the ns3 server, from the Nameserver IPs page in the main server</li>
<li>Check the report on <a href="http://www.intodns.com/" title="intoDNS">intoDNS</a></li>
</ol>

<h2>Final Tweaks</h2>
<ol>
	
<li>Install CSF; follow these <a href="http://configserver.com/free/csf/install.txt" title="CSF Installation Procedure">steps</a>. Configure as suggested <a href="http://forums.cpanel.net/f5/cpanel-dnsonly-285072.html" title="cPanel Forum">here</a></li>

<li>Disable password access for ssh</li>

<li>Turn off cphulk</li>

<li>Disable MySQL, Exim and Spamassassin</li>

<li>Disable httpd if installed</li>

<li><a href="http://lucrussell.com/how-to-change-the-default-ssh-port/" title="How to Change the Default SSH Port">Change the ssh port from the default</a></li>
<li>Update SOA record defaults with DNS Functions > Edit Zone Templates:
<blockquote>
    SOA Refresh: 1200
    SOA Retry: 120
    SOA Expire: 604800
    SOA Min TTL: 3600
</blockquote>
</li>
</ol>



<h2>Troubleshooting</h2>
<ul>
<li>
Error message "Requires version 8.9 or later": add the IP of the dnsonly server to the cphulk whitelist on the web server. Also check for blocks and add to CSF rules. Then re-add the server to the cluster on the main web server
</li>
</ul>

<h2>Further Reading</h2>
<a href="http://sysadminspot.com/linux/http://sysadminspot.com/linux/advantages-cpanel-clustered-dns-and-setup/" title="sysadminspot">SysAdminSpot</a>
<a href="http://www.dotmagz.com/tutorial/tutorial-advanced/how-to-install-and-configure-cpanel-dns-only-for-dns-cluster" title="sysadminspot">Dotmagz</a>