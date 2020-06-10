# Scheduling: Introduction

Workload Assumptions
Scheduling Metrics
	response time 
	turnaround time
FIFO
SJF
STCF
RR

### summary

Note that the cost of context switching does not arise solely from the
OS actions of saving and restoring a few registers. When programs run,
they build up a great deal of state in CPU caches, TLBs, branch predictors,
and other on-chip hardware. Switching to another job causes this state
to be flushed and new state relevant to the currently-running job to be
brought in, which may exact a noticeable performance cost.


RR is fair but is bad for turnaroud time

The first type (SJF, STCF) optimizes turnaround time, but is bad for response time. 
The second type (RR) optimizes response time but is bad for turnaround.
