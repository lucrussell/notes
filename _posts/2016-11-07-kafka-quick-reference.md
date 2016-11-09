---
ID: 649
post_title: Kafka Quick Reference
author: Luc
post_date: 2016-11-07 20:40:49
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/kafka-quick-reference/
published: true
tags_input:
  - 'a:4:{i:0;s:21:"wpghs_pre_import_args";i:1;s:4:"tags";i:2;s:5:"hello";i:3;s:5:"world";}'
tags:
  - kafka
categories:
  - quick reference
---
## Create A Topic

    ./kafka-topics.sh --create --zookeeper myzookeeper:2181 --replication-factor 3 --partitions 3 --topic mytopic
    

## Delete a Topic

    ./kafka-topics.sh --zookeeper myzookeeper:2181 --delete --topic mytopic
    

## Add a Partition

    ./kafka-topics.sh --zookeeper myzookeeper:2181 --alter --topic mytopic --partitions 2
    

## Describe a Topic

Note this describes all the topics, regardless of what topic is supplied.

    ./kafka-topics.sh --describe mytopic
    

## Reassign partitions

Create a file `reassign.json`:

    { "version":1, "partitions":
    [{"topic":"my-topic", "partition":0, "replicas":[0,1,2] }] }
    

Then execute:

    ./kafka-reassign-partitions.sh --zookeeper myzookeeper:2181 --reassignment-json-file reassign.json --execute
    

## Checking Lag

A simple solution for quickly checking lag is as follows. However, a longer term solution is to set up a Grafana instance and report lag to this using statsd.

    ./kafka-consumer-offset-checker.sh --zookeeper myzookeeper:2181 --group my_group_id --topic mytopic
    

## How to Set Up librdkafka with Pykafka

Follow [this reference][1].

In summary:

        git clone https://github.com/edenhill/librdkafka.git
        cd librdkafka/
        ./configure
        make
        sudo make install
    

Then:

    git clone https://github.com/Parsely/pykafka.git
    cd pykafka
    python setup.py develop

The last part, calling `setup.py develop` to put pykafka in develop mode, is necessary for creating the link between the two.

 [1]: https://gist.github.com/yungchin/0b107fd9f4e532de2da5