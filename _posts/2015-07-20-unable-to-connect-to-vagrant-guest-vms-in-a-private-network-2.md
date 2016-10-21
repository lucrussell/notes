---
ID: 597
post_title: >
  Unable to Connect to Vagrant Guest VMs
  in a Private Network
author: Luc
post_date: 2015-07-20 20:24:05
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/unable-to-connect-to-vagrant-guest-vms-in-a-private-network-2/
published: true
en_guid:
  - cd50e050-fefa-4641-a38f-8984bd6c803f
en_modified:
  - "1437665010000"
---
<p>I had a problem connecting to a vagrant virtualbox cluster from the host (OS X 10.10.4 Yosemite).</p>

<p>There are three hosts set up as a vagrant private_network, each having an assigned IP in the range 192.168.37.2 - 192.168.37.4</p>

<p>The virtual network I wanted to connect to (vboxnet0) had a status of Up and the hosts were running. I could connect with <code>vagrant ssh</code> to all of the hosts in the network, but I was unable to ping the virtual host from the host OS.</p>

<p>arp -a showed no entry for the virtual network (vboxnet0):</p>

<pre><code>? (192.168.0.1) at 14:cc:20:4c:37:40 on en0 ifscope [ethernet]

? (192.168.0.100) at b8:e9:37:ec:1c:c4 on en0 ifscope [ethernet]

? (192.168.0.106) at 14:10:9f:de:62:e7 on en0 ifscope permanent [ethernet]

? (192.168.0.255) at ff:ff:ff:ff:ff:ff on en0 ifscope [ethernet]
</code></pre>

<p><code>vboxmanage list hostonlyifs</code> showed six other virtual networks setup, most with status Down, possibly from other vagrant installations</p>

<p>Running these steps fixed it:</p>

<ol>
<li><p>Shutdown all nodes with <code>vagrant halt</code></p></li>
<li><p>Remove all the virtual networks with <code>vboxmanage hostonlyif remove vboxnet0</code> for every network returned by <code>vboxmanage list hostonlyifs</code></p></li>
<li><p>Recreate with <code>vboxmanage hostonlyif create</code>. This recreated the vboxnet0 network which was the only one I was interested in</p></li>
<li><p>Recreate with <code>vboxmanage hostonlyif ipconfig vboxnet0 &ndash;ip 192.168.37.1</code></p></li>
</ol>

<p>This seems to reset the state, now I can connect to each of the hosts in the network.</p>