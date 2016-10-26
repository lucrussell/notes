---
ID: 641
post_title: SVN Quick Reference
author: Luc
post_date: 2013-10-26 00:47:56
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/svn-quick-reference/
published: true
tags_input:
  - 'a:4:{i:0;s:21:"wpghs_pre_import_args";i:1;s:4:"tags";i:2;s:5:"hello";i:3;s:5:"world";}'
tags: [ ]
categories:
  - quick reference
---
# SVN Quick Reference

## Checkout

Checkout to a new directory:

    svn checkout https://svn.com/my-project/trunk my-project
    

## Commit

    svn commit -m "Updated some files"
    

## History of a File, Limited to 5 Entries

    svn log myfile.txt -l 5
    

## Diff Two Revisions

    svn diff myfile.txt -r 55827:55687
    

## Search Log Messages for a Jira

    svn log -v --stop-on-copy $SVNROOT/my-project  | grep JIRA-380
    

## Log All Commit Messages for a Branch

    svn log -v --stop-on-copy $SVNROOT/my-project/branches/JIRA-295_4_Branch/my-project > commit_messages.txt
    

## All Java Files Related to a Set of Jira Ids

Given a log of all commit messages:

    grep -A2 -B2 'JIRA-314|JIRA-380' commit_messages.txt | grep java 
        | cut -d'.' -f1 | awk -F'/' '{ print $NF} '
    

## Show Every Commit Made by the Specified User

    svn log | sed -n '/username/,/-----$/ p'
    

## Get Details for a Specific Revision

    svn log -v -r <revision>
    

## Show Latest Changes

    svn log -l 5
    

## Get a List of Local Changes

    svn status | awk '{print $NF}'
    

## Get a Change Related to a Jira

    svn log -v --stop-on-copy $SVNROOT/project  | grep "JIRA-123" -A2 -B2
    

## Add to svn Ignore

    svn propset svn:ignore app-classpath .
    

See [here][1] for more details.

## Move a File or Directory

    svn move -m "JIRA-847: Moving my-project to correct location" https://svn.com/my-project https://svn.com/trunk/my-project
    

## Last Changed Revision

    svn info $SVNROOT/my-project | grep 'Last Changed Rev'
    Last Changed Rev: 59199
    

## Diff

    svn diff -r 57859:58002
    svn log -v -q -r 58936:59072 $SVNROOT/my-project/trunk
    

## Diff Two Tags

    svn log -v -q -r 111:222 http://my-project/trunk
    

See [here][2] for more details.

 [1]: http://stackoverflow.com/questions/116074/how-to-ignore-a-directory-with-svn
 [2]: http://stackoverflow.com/questions/3270322/subversion-how-to-find-the-differences-between-two-tags