To implement virtualization of the CPU, and to implement it well, the OS will need both some low-level machinery(context switch) as well as some high-level intelligence(sche policy).

## 4.1 The Abstraction: A Process

what constitutes a process

- memory
  - code data stack
- CPU register
- persistent storage device

## 4.2 Process API

- creat
- wait
- notify
- sleep
- exit

## 4.3 Process Creation

> how programs are transformed into processes
>
> fork 做了什么

the process of **loading a program and static data into memory** requires the OS to read those bytes from disk and place them in memory somewhere.

Some memory must be allocated for the program’s run-time stack (or just **stack**).

The OS may also create some initial memory for the program’s **heap**.

The OS will also do some other initialization tasks, particularly as related to **input/output (I/O).**

to **start** the program running at the entry point

## 4.4 Process States

- running 
- ready
- blocked

## 4.5 Data Structures

**Zombie process**

This final state can be useful as it allows other processes (usually the parent that created the process) to examine the return code of the process and see if it the just-finished process executed successfully

