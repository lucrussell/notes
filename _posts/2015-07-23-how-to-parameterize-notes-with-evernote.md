---
ID: 601
post_title: How To Parameterize Notes with Evernote
author: Luc
post_date: 2015-07-23 14:54:31
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/how-to-parameterize-notes-with-evernote/
published: true
en_guid:
  - a31240a4-6726-4932-8898-3ccd70c3141c
en_modified:
  - "1437665968000"
---
<p>Evernote doesn't explicitly allow parameterized files. By this, I mean you can't put a variable in a file and have a real value substituted in when you choose. This is useful for documentation where you need to specify slightly different values each time, but don't want to copy and paste the whole document, e.g. troubleshooting documentation, or deployment documents with hostnames. Here's an idea for working around the limitation:</p>

<h2>Steps</h2>

<p>Set up http://www.geeknote.me/ so you can extract notes from ENML as text</p>

<p>Write a document containing some variables in format <code>$my_variable</code></p>

<p>Set the variables in your shell: <code>myvariable=foo</code></p>

<p>Run a command like this to substitute:</p>

<pre><code>geeknote find &ndash;search "My Generic Document"

geeknote show 1 &gt; tmp.txt; while read line; do eval echo "$line"; done  out.txt; rm tmp.txt`
</code></pre>

<p>Enjoy your substituted document in <code>out.txt</code></p>

<h2>Example</h2>

<p>Create a new note called Deployment Troubleshooting. Add something to the content:</p>

<pre><code> When your deployment fails, first check logs in /var/log/$app.log on $hostname
</code></pre>

<p>Set the hostname variable in your shell:</p>

<pre><code> app=myapp; hostname=123.4.5.6
</code></pre>

<p>Run the command to substitute:</p>

<pre><code>geeknote find &ndash;search "Deployment Troubleshooting"

geeknote show 1 &gt; tmp.txt; while read line; do eval echo "$line"; done  out.txt; rm tmp.txt

cat out.txt

&mdash;&mdash;&mdash;&mdash;&mdash;&ndash; CONTENT &mdash;&mdash;&mdash;&mdash;&mdash;&ndash;

When your deployment fails, first check logs in /var/log/myapp.log on 123.4.5.6
</code></pre>