---
author: Luc
layout: post
published: true
tags:
  - kafka
categories:
  - kafka
---
Kafkacat is a useful tool for working with Kafka brokers. It's quick and very simple to use. This is a cheatsheet of some useful commands.

## Produce

    $ echo "foo" | kafkacat -b localhost:9092 -t mytopic

## Consume

    kafkacat -C -b localhost:9092  -t mytopic

## List Topics

    kafkacat  -b localhost:9092 -L -t mytopic

## Read messages from a file, each message separated by a newline

    kafkacat -P -l -b kafka:9092 -t mytopic myfile

## Generate a Test File of Messages
Given a file containing a `DATE` variable, generate a set of messages with incrementing timestamp, for use with the previous example:

    for i in {1..5000}; do DATE=`date -u +%d/%b/%Y:%H:%M:%S`; sed "s~DATE~$DATE~" template.msg >> myfile; done
    
## Read the Last n Messages from Partition n
This example uses the `-o` flag to read from a specified offset. Specifying `-3` allows retrieval of the last 3 messages. The `-p` option targets partition 0:

    kafkacat -C -b kafka -t mytopic -o -3 -e -p 0
