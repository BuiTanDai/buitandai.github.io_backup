---
layout: post
title: How does the OS handle scheduling? (single processor)
description: 
summary: 
tags: [operating-system]
---

How does the OS handle scheduling? (single processor)

![image info](/_image/index.jpeg)


One of scheduler, Multi-level feedback queue.

It's used in BSD UNIX derivatives, Solaris, Windows NT and subsequent Windows operating system.

We need to know two metrics that is considered to measure the performance of a scheduler.
1. Time turnaround = Time completion - Time arrival 
2. Time response = Time first run - Time arrival

Time slice: a very short timer for OS to retain control the system. When it time out, OS could switch context (do another job) or continue doing current job. 
This decision totally depend on sheduler.

So, what is Multi-level feedback queue (MLFQ)?

MLFQ is a sheduler that:
- minimize the turnaround time without a priori knowledge of job length.
- minimize the response time for interactive job.

There are many approaches but have same basic rules:
- Rule 1: if Priority(A) > Priority(B), run A first
- Rule 2: if Priority(A) = Priority(B), A & B run in Round Robin
- Rule 3: when a job enter the system, it is placed at the highest priority queue.
- Rule 4: Once a job uses up its time, its priority is reduced (ex: it moves down one queue)
- Rule 5: After some time period S, move all the jobs in the system to the topmost queue.

the higher queue, the shorter timer slice.

=> this sheduler pays attention to how the jobs behave overtime and treat them accordingly.


