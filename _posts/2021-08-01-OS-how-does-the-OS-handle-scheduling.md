---
layout: post
title: How does the OS handle scheduling? (single processor)
description: 
summary: 
tags: [operating-system]
---

How does the OS handle scheduling? (single processor)

We need to know two metrics that is considered to measure the performance of a scheduler.
1. Time turnaround = Time completion - Time arrival 
2. Time response = Time first run - Time arrival

Some basic scheduler:

• FIFO: the most basic algorithm but perform poorly when have a long run-time task in the first queue

![image info](https://raw.githubusercontent.com/BuiTanDai/buitandai.github.io/main/_image/OS/Scheduler/FIFO-isnot-great.PNG)
	
	Time turnaround = (100 + 110 + 120)/3 = 110

• SJF (shortest job first) solve the problem above but it has disadvantage if task B, C come later after A.

![image info](https://raw.githubusercontent.com/BuiTanDai/buitandai.github.io/main/_image/OS/Scheduler/Shortest-Job-First-example.PNG)
	Time turnaround  = (10 + 20 + 120)/3 = 50

• STCF (Shortest Time-to-Completion First) solve the problem above by when job B, C come, this algorithm compute time to complete of each job, and select shortest time-to-complete to run first

![image info](https://raw.githubusercontent.com/BuiTanDai/buitandai.github.io/main/_image/OS/Scheduler/Shortest-Time-to-Complete-First-example.PNG)
    Time turnaround  = (120 + (20 - 10) + (30 - 10))/3 = 50

Consider metric Response time:

• Round Robin run a job for a time slice, then switch to the next job in the run queue.

![image info](https://raw.githubusercontent.com/BuiTanDai/buitandai.github.io/main/_image/OS/Scheduler/Round-Robin.PNG)
not good for Time turnround = (13 + 14 + 15)/3 = 14
but good for Response time.

Must be consider the value of time slice, too small, cost time to switch context, too big, the system is no longer responsive.
 
//To-do when process need I/O

All task above is known length task. If we don't know, how could we build the scheduler with good result
=> we need to build a scheduler that uses recent past to predict the future.


That is Multi-level feedback queue.

It's used in BSD UNIX derivatives, Solaris, Windows NT and subsequent Windows operating system.

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


