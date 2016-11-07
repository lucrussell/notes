---
ID: 651
post_title: Kafka Troubleshooting Notes
author: Luc
post_date: 2016-11-07 20:40:50
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/kafka-troubleshooting-notes/
published: true
tags_input:
  - 'a:4:{i:0;s:21:"wpghs_pre_import_args";i:1;s:4:"tags";i:2;s:5:"hello";i:3;s:5:"world";}'
tags: [ ]
categories:
  - errors and problems
---
## Something Wrong With One Broker in a Cluster

### Problem

Consumer connected to a broker but not receiving messages. Looking at various topics, broker 0 is marked as an out of sync replica, e.g.:

`./kafka-topics.sh --describe my-topic --zookeeper myzk:2181/kafka
Topic: my-topic        Partition: 6    Leader: 4       Replicas: 0,4,1 Isr: 4,1
...
Topic: __consumer_offsets       Partition: 1    Leader: 2       Replicas: 0,1,2 Isr: 2,1` Notice '0' is missing from the `Isr` list above.

Also, I tried publishing a test message manually to the topic using `broker-0` and it didn't seem to arrive. Lag did not increase, whereas lag does increase if I publish directly to `broker-4` instead.

### Solution

In this case, the problem was caused by some internal problem in the broker which caused it to drop out of the broker cluster. Restarting the broker resolved the immediate problem. However, the (Pykafka) consumers repeatedly attempted to reset to offset `-1` on startup. To resolve this, the consumers can be force reset to a specific offset (assuming there is a record somewhere of the latest offset that has actually been consumed). There is a simple script [here][1] to reset offsets.

 [1]: https://github.com/lucrussell/kafka-tools