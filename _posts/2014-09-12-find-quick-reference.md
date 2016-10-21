---
ID: 542
post_title: Find Quick Reference
author: Luc
post_date: 2014-09-12 16:43:53
post_excerpt: |
  |
    This is a quick cheat sheet of my favourite find commands.
layout: post
permalink: >
  http://lucrussell.com/find-quick-reference/
published: true
---
This is a quick cheat sheet of my favourite find commands.

<h3>Find Then Grep</h3> 
 <span class="lang:sh highlight:0 decode:true  crayon-inline " >find . -name file.* -exec grep -Hn thingtogrep {} \;</span> 



<h3>Find By Name<h3>
<span class="lang:sh highlight:0 decode:true  crayon-inline " >
find . -name "MyCProgram.c"
</span>

<span class="lang:sh highlight:0 decode:true  crayon-inline " >
find . -name "proto*"
</span>

<h3>Find And Copy Somewhere</h3>
<span class="lang:sh highlight:0 decode:true  crayon-inline " >
find . -name <file> -exec cp {} <target dir>/ \;
</span>

<span class="lang:sh highlight:0 decode:true  crayon-inline " >
find . -name wget* -exec cp {} $TEMP/wget \; (confirmed)
</span>

<h3>Find And Delete</h3>
<span class="lang:sh highlight:0 decode:true  crayon-inline " >
find . -name ".svn" -exec rm -rf {} \;
</span>
This finds and deletes svn directories. See link on <a href="http://www.cyberciti.biz/faq/linux-unix-how-to-find-and-remove-files/">Cyberciti</a> for more details.


<h3>Find And Open A File</h3>
<span class="lang:sh highlight:0 decode:true  crayon-inline " >
find ~ -name "file.xml" -exec vim {} \;
</span>

<h3>Find And Move Somewhere</h3>
<span class="lang:sh highlight:0 decode:true  crayon-inline " >
find -name "*.java" -exec mv {} /cygdrive/c/temp \;
</span>

<h3>Find And Replace In Files</h3>
<span class="lang:sh highlight:0 decode:true  crayon-inline " >
find . -type f -print | xargs sed -i 's/thing_to_replace/another_thing/g'
</span>
Or
<span class="lang:sh highlight:0 decode:true  crayon-inline " >
find . -type f -exec sed -i 's/ugly/beautiful/g' {} \;
</span>
Note the -i is for edit in place, not case-insensitive.

<h3>Run A Command On A File</h3>
<span class="lang:sh highlight:0 decode:true  crayon-inline " >
find <CONDITION to Find files> -exec <OPERATION> \;
</span>

<span class="lang:sh highlight:0 decode:true  crayon-inline " >
find -iname "MyCProgram.c" -exec rm {} \;
</span>

<span class="lang:sh highlight:0 decode:true  crayon-inline " >
find -iname "MyCProgram.c" -exec md5sum {} \;
</span>

<h3>Finding the Top 5 Big Files</h3>
<span class="lang:sh highlight:0 decode:true  crayon-inline " >
find . -type f -exec ls -s {} \; | sort -n -r | head -5
</span>

<span class="lang:sh highlight:0 decode:true  crayon-inline " >
find . -type f -exec ls -s {} \; | sort -n -r | head -10 > ~/largefiles.txt &
</span>

<h3>Find Files Based on File-Type</h3>
<span class="lang:sh highlight:0 decode:true  crayon-inline " >
find . -type s
</span>

<h3>Show files which are modified after the specified file</h3>
<span class="lang:sh highlight:0 decode:true  crayon-inline " >
find -newer ordinary_file
</span>
<h3>Find Files Larger Than The Given Size</h3>
<span class="lang:sh highlight:0 decode:true  crayon-inline " >
find ~ -size +100M
</span>
<h3>Find Files Whose Content Was Updated Within The Last...</h3>

<span class="lang:sh highlight:0 decode:true  crayon-inline " >
1 hour: find . -mmin -60
</span>

<span class="lang:sh highlight:0 decode:true  crayon-inline " >
1 day: find / -mtime -1
</span>

<h3>Exclude a Directory</h3>
<span class="lang:sh highlight:0 decode:true  crayon-inline " >
find .  -path './excludedir' -prune -o -name "*" -print
</span>

<h3>Search All jar Files In A Directory For A Class Name</h3>
<span class="lang:sh highlight:0 decode:true  crayon-inline " >
find . -type f -name '*.jar' -print0 | xargs -n1 -0i sh -c 'jar tf "{}" | grep -q AQOracleDriver && echo "{}"'
</span>

<h3>Avoiding Permission denied messages</h3>
Add this:
<span class="lang:sh highlight:0 decode:true  crayon-inline " >
-perm -a+r -perm /a+w ! -perm /a+x
</span>