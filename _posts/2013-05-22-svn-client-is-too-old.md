---
ID: 382
post_title: 'SVN: Client is too old'
author: Luc
post_date: 2013-05-22 07:34:46
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/svn-client-is-too-old/
published: true
---
     <code>[exec] svn: This client is too old to work with working copy ...  You need
     [exec] to get a newer Subversion client, or to downgrade this working copy.
     [exec] See http://subversion.tigris.org/faq.html#working-copy-format-change
     [exec] for details.</code>

Simplest fix; delete everything under this path and re-checkout.