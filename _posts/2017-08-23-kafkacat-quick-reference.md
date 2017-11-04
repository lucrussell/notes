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
[TOC levels=1-3]: # "Contents"

# Contents
- [Produce](#produce)
- [Consume](#consume)
- [List Topics](#list-topics)
- [Read Messages From File](#read-messages-from-file)
- [Generate a Test File of Messages](#generate-a-test-file-of-messages)
- [Read the Last n Messages from Partition n](#read-the-last-n-messages-from-partition-n)


[kafkacat](https://github.com/edenhill/kafkacat) is a useful tool for working with Kafka brokers. It's quick and very simple to use. This is a cheatsheet of some useful commands.

## Produce

    $ echo "foo" | kafkacat -b localhost:9092 -t mytopic

## Consume

    kafkacat -C -b localhost:9092  -t mytopic

## List Topics

    kafkacat  -b localhost:9092 -L -t mytopic

## Read Messages From File
Read messages from a file, with each message separated by a newline:

    kafkacat -P -l -b kafka:9092 -t mytopic myfile

## Generate a Test File of Messages
Given a file containing a `DATE` variable, generate a set of messages with incrementing timestamp, for use with the previous example:

    for i in {1..5000}; do DATE=`date -u +%d/%b/%Y:%H:%M:%S`; sed "s~DATE~$DATE~" template.msg >> myfile; done
    
## Read the Last n Messages from Partition n
This example uses the `-o` flag to read from a specified offset. Specifying `-3` allows retrieval of the last 3 messages. The `-p` option targets partition `0`:

    kafkacat -C -b kafka -t mytopic -o -3 -e -p 0