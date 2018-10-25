---
ID: 808
post_title: >
  Consuming from NSQ to Hadoop HDFS with
  Apache Flume
author: Luc
post_excerpt: ""
layout: post
permalink: >
  https://lucrussell.com/consuming-from-nsq-to-hadoop-hdfs-with-apache-flume/
published: true
post_date: 2018-10-25 23:32:52
---
I was working on a prototype for consuming from [NSQ](https://nsq.io/) to the Hadoop [HDFS](https://hortonworks.com/apache/hdfs/) file system with [Apache Flume](https://flume.apache.org/). I couldn't find much information, so I made a small [project](https://github.com/lucrussell/flume-nsq).

Below are a few extra notes about nsq and the project.

* `docker-flume/Dockerfile` builds a container which includes Flume, nsq and Hadoop core necessary for persisting files to HDFS
* In order to be able to quickly modify some files in the built docker container, some extra paths are mapped in the `docker-compose.yml`:
  * Adding the start-flume.sh script allows updating the classpath to quickly add libraries and restart the container.
  * Adding the flume/flume.conf path means the flume config can be adjusted and the container restarted, without requiring a container rebuild.
* In flume.conf `docker.sources.r1.command` specifies `nsq_tail`. While this is a quick way to consume from nsq, it is possibly not a reliable technique to use in a production environment.
* nsq doesn't appear to have a mechanism for resuming from an offset, like Kafka. This means there could be gaps in data if a consumer goes down and comes back up. In this sense, nsq has similarities to high volume messaging systems like RabbitMQ or ZeroMQ, which provide fewer message durability guarantees than Kafka.