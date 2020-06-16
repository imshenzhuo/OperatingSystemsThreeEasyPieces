# Scheduling: The Multi-Level Feedback Queue
design a scheduler

- minimizes response time for **interactive jobs** 
- minimizing **turnaround time** without a priori knowledge of job length

## 1 Basic Rules

the MLFQ has a number of distinct queues, each assigned a different priority level.

- Rule 1: If Priority(A) > Priority(B), A runs (B doesn’t).
- Rule 2: If Priority(A) = Priority(B), A & B run in RR.

how the scheduler sets priorities?

> based on its observed behavior

- keep its priority high, If, for example, a job repeatedly relinquishes the CPU while waiting for input from the keyboard
- reduce its priority a job uses the CPU intensively for long periods of time.

## 2 Attempt #1: How to Change Priority

- Rule 3: When a job enters the system, it is placed at the highest priority (the topmost queue).
- Rule 4a: If a job uses up an entire time slice while running, its priority is reduced (i.e., it moves down one queue).
- Rule 4b: If a job gives up the CPU before the time slice is up, it stays at the same priority level.

一个进程的优先级自顶而下, 如果一个交互式进程偶尔计算/一个CPU进程偶尔做IO, 就没有优先级提升的机会只能在下面了吗?

### problem

1. starvation: if there are “too many” interactive jobs...
2. game the scheduler (只要调度程序去猜,用户程序就能模仿)
3. a program may change its behavior over time (优先级只下不上)

## 3 Attempt #2: the Priority Boost

let’s just do something simple: throw them all in the topmost queue

- Rule 5: After some time period S, move all the jobs in the system to the topmost queue.

解决了问题1和问题3

> what should S be set to?

- set too high, long-running jobs could starve
- too low, and interactive jobs may not get a proper share of the CPU

## 4 Attempt #3: Better Accounting

- Rule 4: Once a job uses up its time allotment at a given level (regardless of how many times it has given up the CPU), its priority is reduced (i.e., it moves down one queue).

这样虽然真的interactive process和普通process都会"下沉", 但是普通process会下沉的快

## 5 Tuning MLFQ And Other Issues

> 调参由来已久

- how many queues should there be? 
- How big should the time slice be per queue? 
- How often should priority be boosted in order to avoid starvation and account for changes in behavior?

eg 优先级越高, 时间片越短

有的系统(Solaris)很容易配置--通过配置文件直接配置, 有点系统(FreeBSD)高级一些, 用的数学公式, 有的调度器的最高优先级只能是操作系统, 有的系统可以允许用户调整优先级(nice调用)

## 6 Summary

MLFQ: it has *multiple levels* of queues, and uses *feedback* to determine the priority of a given job.

- Rule 1: If Priority(A) > Priority(B), A runs (B doesn’t).
- Rule 2: If Priority(A) = Priority(B), A & B run in RR.
- Rule 3: When a job enters the system, it is placed at the highest priority (the topmost queue).
- Rule 4: Once a job uses up its time allotment at a given level (regardless of how many times it has given up the CPU), its priority is reduced (i.e., it moves down one queue).
- Rule 5: After some time period S, move all the jobs in the system to the topmost queue.