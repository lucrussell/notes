---
ID: 297
post_title: 'Cygwin: What is Locking a File'
author: Luc
post_date: 2013-04-09 16:25:59
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/cygwin-what-is-locking-a-file/
published: true
---
You need sysinternals 'Handle' first

cd /cygdrive/c/Tools
./handle.exe "absolute path in Windows format" (needs the quotes)
e.g. ./handle.exe  "C:\Development\workspace\my_project\"