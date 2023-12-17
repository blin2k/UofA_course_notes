# Intro
In multi-programming systems, when there are more than one processes are ready, the OS must decide which one to run next.

This decision is made by ==scheduler==, using scheduling algorithm or scheduling discipline.
- concerned with deciding ==policy==
- not providing a mechanism
	- the dispatcher is the mechanism

# Policy vs. Mechanism
- separate the decision making from the execution
	- execution is done by the dispatcher
- kernel with scheduling algorithm can decide what process to run next
- processes can do the decision making for their threads

# Basic
CPU is the most important resource scheduled before used. But other criteria may be important too (memory).

The basic idea is to keep the CPU busy as much as possible by executing a process until it must wait for an event and then switch to another process.
- processes alternate between consuming CPU cycles and performing IO
	- CPU-burst
	- IO-burst

# Classification
The system may try to guess
- performance characteristics over time
- duration of the next CPU burst 
	- from the history
- the average over a time period
	- Simple Moving Average (MVA)
- a dynamic average by decaying the value of older data points
	- Exponential Moving Average (EMA)

# Types of Scheduling
- long term
	- done when a new process is created
	- control the degree of multi-programming by initiating processes
- medium term
	- suspending or resuming processes by swapping them out of or into memory
- short term
	- most frequently
	- decides which process to execute next

![[Pasted image 20231214235347.png]]
Long-term scheduler controls the number of concurrent jobs
- admit more jobs when resource utilization is low
- block the incoming jobs from entering the queue otherwise

Medium-term scheduler swaps suspended job out of the memory to make space.

# Short-Term Scheduling Criteria
goal
- optimize the system performance
	- high throughput
- provide response service
	- low latency

criteria
- CPU utilization
- IO device throughput
- total service time
- responsiveness
- fairness
- deadlines

They may be conflict
- utilization increases by increasing the number of active processes
- response time deteriorate

# Performance Metrics
- turnaround time
	- enter to complete
	- lower is better
- waiting time
	- total amount of time spend in READY state
	- lower is better
- throughput
	- number of completed jobs per time period
	- higher is better

# Scheduling Policies
- preemptive
	- force the currently active process to release the CPU on certain events
	- clock interrupt, IO interrupts, or system call
	- algorithm
		- Round-Robin (RR)
			- running jobs periodically
			- suspend the current job when the reserved quantum is exhausted
				- the issue is the length of the quantum
			- the job is put at the end of the READY queue
		- Priority
			- preemption of current process when higher priority process arrives
			- priority remains in the READY queue
			- may starving the low priority ones
				- add a time component to the priority (the age factor)
- non-preemptive
	- let the current process run until it blocks, waiting, or terminates
	- algorithm
		- First-Come-First-Served (FCFS)
			- short job suffer
		- Shortest Job First (SJF
			- need to know the processing time
			- long job starve

CPU bursts are always short
- no need to guess or estimate
- they should be ahead of everything else

# Multi-Level Queue
Maintaining separate READY queues for each type of job class and apply different scheduling algorithms to each.
![[Pasted image 20231215011903.png]]

# Multi-Level Feedback Queue
A variation of MLQ
- jobs are not permanently assigned to a queue when they enter the system
- move to another queue with longer quantum and lower priority when its quantum is exhausted
![[Pasted image 20231215012154.png]]
The last level usually uses FCFS

# Real-Time System
Controls or monitors external events that have their own timing requirements.

Task
- process in RT
- associate with a deadline
	- specifying either a start time or a completion time

- hard RT
	- must meet the deadline
		- time critical
	- often, an external factor determines the deadlines
- soft RT
	- meeting a deadline is desirable but not  mandatory
		- better performance


standard OS
- capacity
	- high throughput
	- statistically good utilization of all equipment
	- low overhead
- responsiveness
	- low average turnaround time
	- low average response time
- overload
	- fair performance degradation

RT OS
- capacity
	- number of context switches per second
	- number of interrupts per second
	- scheduleability
- responsiveness
	- worst-case delay
	- low variance 
	- predictable behavior
- overload
	- stability
	- unaffected performance for critical tasks