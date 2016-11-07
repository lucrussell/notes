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

## Why

*   If you rely on a DNS service running on your web server, every query must go to this server, meaning the queries will be slower for geographically remote users.
*   Outages on your web server will affect DNS resolution which is used for other functions, e.g email delivery. If your web server and DNS are hosted together, and your web server goes down for a few minutes, mail to that domain will be returned to the sending server's queue and marked as a permanent failure. If the DNS service is clustered on separate servers, even if your web server goes down for a few minutes, the DNS server will still be running.
*   You could use a 3rd party DNS service like [DNS Made Easy](http://dnsmadeeasy.com "DNS Made Easy"). However, you'll have to manually update this 3rd party service each time you want to modify account details. cPanel will manage this for you by synchronising changes out to DNSONLY servers.

## Steps

These steps apply if you have an existing cPanel WHM web server, and you want to create a DNS cluster, adding a new cPanel DNSOnly server.

1.  Obtain a new server, a hardware spec of 256mb memory, 10/15GB disk should be sufficient. [Low End Talk](http://www.lowendtalk.com/categories/offers "Low End Talk") sometimes have offers for this sort of server
2.  Install pre-requisites if necessary. On a fresh Centos 6.4 install, I needed:

> `yum install wget yum install perl`

4.  Install cPanel DNSOnly:

> `cd /home wget -N http://httpupdate.cpanel.net/latest-dnsonly sh latest-dnsonly`

6.  Go to https://your_ip:2087/ and follow the wizard
7.  On your existing cPanel WHM server (the original web server):

    *   Add your new server under clustering, set it to sync
    *   Now follow [these steps](http://www.docs.cpanel.net/twiki/bin/view/AllDocumentation/WHMDocs/ConfigureCluster "cPanel Documentation") from the cPanel documentation
    *   Set the server you're adding to Synchronize Changes
    *   Go to Edit DNS Zone and add a new NS record, pointing to the IP of the new DNS server

8.  On the new DNS server:

    *   Go to WHM > Configure Cluster, check that the main server appears and the DNS role is Standalone. Generally it is not recommended setting up the DNS server to synchronize data to a web server

## Check the Setup

1.  Log in to WHM on the main server and Synchronize one zone to all servers, with a test domain
2.  ssh into the dnsonly server, `ls /var/named/*.com.db` and you should see the synchronised account has been sent over
3.  You should also see the new zone on the ns3 server, from the Nameserver IPs page in the main server
4.  Check the report on [intoDNS](http://www.intodns.com/ "intoDNS")

## Final Tweaks

1.  Install CSF; follow these [steps](https://download.configserver.com/csf/install.txt "CSF Installation Procedure"). Configure as suggested [here](http://forums.cpanel.net/f5/cpanel-dnsonly-285072.html "cPanel Forum")
    * You may need to use `install.cpanel.sh` as the entry installation script.
    * You may need to edit the script to reduce the required memory on some hosts.
2.  Disable password access for ssh
3.  Disable httpd if installed
4.  [Change the ssh port from the default](http://lucrussell.com/how-to-change-the-default-ssh-port/ "How to Change the Default SSH Port")
5.  Update SOA record defaults with DNS Functions > Edit Zone Templates:

    > SOA Refresh: 1200 SOA Retry: 120 SOA Expire: 604800 SOA Min TTL: 3600

## Troubleshooting

*   Error message "Requires version 8.9 or later": add the IP of the dnsonly server to the cphulk whitelist on the web server. Also check for blocks and add to CSF rules. Then re-add the server to the cluster on the main web server

## Further Reading

* [SysAdminSpot](http://sysadminspot.com/linux/http://sysadminspot.com/linux/advantages-cpanel-clustered-dns-and-setup/ "sysadminspot") 
* [Dotmagz](http://www.dotmagz.com/tutorial/tutorial-advanced/how-to-install-and-configure-cpanel-dns-only-for-dns-cluster "sysadminspot")