---
ID: 680
post_title: Kafkacat Quick Reference
author: Luc
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/kafkacat-quick-reference/
published: true
post_date: 2017-08-23 15:42:59
tags:
  - kafka
categories:
  - kafka
---
<h1>Kafkacat Quick Reference</h1>

<a href="https://github.com/edenhill/kafkacat">kafkacat</a> is a useful tool for working with Kafka brokers. It's quick and very simple to use. This is a cheatsheet of some useful commands.

<h2>Produce</h2>

<pre><code>$ echo "foo" | kafkacat -b localhost:9092 -t mytopic
</code></pre>

<h2>Consume</h2>

<pre><code>kafkacat -C -b localhost:9092  -t mytopic
</code></pre>

<h2>List Topics</h2>

<pre><code>kafkacat  -b localhost:9092 -L -t mytopic
</code></pre>

<h2>Read messages from a file, each message separated by a newline</h2>

<pre><code>kafkacat -P -l -b kafka:9092 -t mytopic myfile
</code></pre>

<h2>Generate a Test File of Messages</h2>

Given a file containing a <code>DATE</code> variable, generate a set of messages with incrementing timestamp, for use with the previous example:

<pre><code>for i in {1..5000}; do DATE=`date -u +%d/%b/%Y:%H:%M:%S`; sed "s~DATE~$DATE~" template.msg &gt;&gt; myfile; done
</code></pre>

<h2>Read the Last n Messages from Partition n</h2>

This example uses the <code>-o</code> flag to read from a specified offset. Specifying <code>-3</code> allows retrieval of the last 3 messages. The <code>-p</code> option targets partition 0:

<pre><code>kafkacat -C -b kafka -t mytopic -o -3 -e -p 0
</code></pre>