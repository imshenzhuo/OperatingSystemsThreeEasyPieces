# Scheduling: The Multi-Level Feedback Queue
design a scheduler

- minimizes response time for **interactive jobs** 
- minimizing turnaround time without a priori knowledge of job length

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

1. starvation
2. game the scheduler

都可以添加进程的运行时间, 根据运行时间调整优先级解决

## 3 Attempt #2: the Priority Boost

let’s just do something simple: throw them all in the topmost queue

- Rule 5: After some time period S, move all the jobs in the system to the topmost queue.

> what should S be set to?

## 4 Attempt #3: Better Accouting

