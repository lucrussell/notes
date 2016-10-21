---
ID: 356
post_title: >
  What is the Difference Between Queue
  Priority and Order?
author: Luc
post_date: 2013-05-01 07:39:03
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/what-is-the-difference-between-queue-priority-and-order/
published: true
---
Note to self: You should not use message priority as a proxy for message order; this will only work in a single consumer situation. E.g.
    - Assume high priority messages have to be processed before low
    - You have 10 consumers
    - 11 messages arrive, 10 high, 1 low priority
    - All consumers start processing a high priority message
    - Consumer 3 finishes his high priority message and starts on the next message (the low priority one)
    - But the high priority message this message depends on has not been finished yet