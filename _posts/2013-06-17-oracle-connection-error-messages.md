---
ID: 433
post_title: Oracle Connection Error Messages
author: Luc
post_date: 2013-06-17 08:54:17
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/oracle-connection-error-messages/
published: true
---
A quick summary of what might go wrong when trying to connect to an Oracle database. Based on <a title="edstevensdba" href="http://edstevensdba.wordpress.com/2011/02/09/sqlnet_overview/">this excellent article</a>. Read the whole thing, this is just a quick reference.

<style>
table
{
border-collapse:collapse;
}
table, td, th
{
border:1px solid black;
padding:5px;
}
</style>
<table>
<tbody>
<tr>
<td>Error Code</td>
<td>Message</td>
<td>Translation</td>
</tr>
<tr>
<td>ORA-12154</td>
<td>TNS:could not resolve the connect identifier specified</td>
<td>No entry with the requested name in tnsnames.ora</td>
</tr>
<tr>
<td>ORA-12545</td>
<td>Connect failed because target host or object does not exist</td>
<td>There is an entry in tnsnames.ora, but the hostname doesn't resolve to an IP, or the IP is bad. The server can't be reached</td>
</tr>
<tr>
<td>ORA-12541</td>
<td>TNS:no listener</td>
<td>All the above are OK, but there is no listener process running on the server we're trying to connect to</td>
</tr>
<tr>
<td>ORA-12560</td>
<td>TNS:protocol adapter error</td>
<td>The connection to the server is OK, and there is a listener process on the target server, but it is running on a different port than that specified in the tnsnames.ora</td>
</tr>
<tr>
<td>ORA-12514</td>
<td>TNS:listener does not currently know of service requested in connect descriptor/td>
<td>We got as far as connecting to the listener process on the server, but the service name in the tnsnames.ora is wrong</td>
</tr>
</tbody>
</table>