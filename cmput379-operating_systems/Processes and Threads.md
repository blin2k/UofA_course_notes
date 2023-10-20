# Process

A process is ==a program in execution==
- the program to be executed
- the data will be needed by the program
- CPU resources (registers)
- data resources required by the program
	- buffer
- status of the execution

## Process vs. Program

A program can invoke several processes.
- multi-threads

A program can be part of a process context
- two process using the same program but offering different arguments

## Uni- vs. Multi

- Uni-programming systems
	- only one process at a time
- Multi-programming systems
	- NOT multi-processing
	- the CPU switches from process to process, running each for a period of time
		- running one and only one process at a time
		- ANALOGY: Draw a dot on a fan, you can a circle when it is on. You did not draw a circle (dots occur at the same time), instead, the same dot frequently shows up at different place. It happens so fast that your brain consider they are not the same dot.

---
# Multiple Processes: One CPU

- fair scheduling
	- each process gets a chance to run
- protection
	- they do not modify each other's state
- shared resources

---
# Process States

The life time of a process can be described by ==a number of states==.

The operation of a multi-programming system can be described by ==a state transition diagram== on the process states.

Most of state transition are internal to the OS and the user has no control.
![[Pasted image 20231019172841.png]]

- new
	- a process being created but not yet included in the pool of executable process
	- resource acquisition
- ready
	- are prepared to execute when given the opportunity
- active
	- currently being executed
- blocked
	- cannot execute until some event occurs
	- stopped
		- special case of blocked
		- being suspended by the operator or the user
- exiting
	- about to be removed from the pool of executable processes
	- resource release

---
# Process Description

Process Control Block
- process state information
	- registers
- process control information
	- priority
	- resources held
	- memory allocated

The OS must know these information to manage and control processes. 

---
# Process Scheduling

To have some process running at all times, the ==dispatcher== module in the OS keeps doing this:

```
loop forever{
	run a process for a while
	stop process and save its state
	load state of another process
}
```

Basically, find a process 
-> load the state
-> run it
-> update and save its state
-> find another process

then back to the first one: load its state

---
# Control of the CPU

The CPU can only run one process at a time, so how to make sure the dispatcher regaining the control?
- trust the process will wake up the dispatcher at the end
- provide a mechanism to wake it up
	- poll
	- alarm clock

---
# Context Switch

Context Switch:
	When an event occurs, the OS saves the state of the active process and restores the state of ISR (interrupt service routine).

Must be saved (Everything that the next process could or will damage)
- program counter
- program status word
- file assess pointer
- memory

The OS should mask all interrupts when saving the state, otherwise it cannot goes back after fixing the interrupt.

---
# Creating a New Process

- build a new one
	- load code and data into memory
	- create a dynamic memory workspace
	- create and initialize the PCB
	- make process known to the dispatcher
- clone an existing one
	- stop current process and save its state
	- make a copy
		- code
		- data
		- dynamic memory workspace
		- PCB
	- make process known to the dispatcher

Who creates the processes?
Every OS has a mechanism to create processes ( fork() ).

Parent and children may need to coordinate with each other ( wait() ).
This is a form of synchronization.

---
# Process Termination

A process enters the exiting state for one of the following reasons
- normal completion
	- executes a system call for termination
		- exit()
- abnormal termination
	- programming error
		- divide by zero
	- runtime
		- out of memory
	- I/O
		- hardware error
	- user intervention
		- kill the process

---
# Threads

The abstraction of a unit of execution. Also referred to as a light-weight process (LWP).

- unit of execution
- belongs to process
	- a process can have multiple threads to take advantage of multi-cores
- collection of local and shared resources

A thread shares its code and data, as well as system resources and other OS related information, with its peer group.
- it makes sense because they are in the same process, so it does not break the security rule

## Threads vs. Process

- They operates in much the same way
	- can be one of the several states
	- executes sequentially
	- can issue system calls
- less expensive
	- no need to spawn a new process
- cheaper switch, thus convenient and efficient
	- switching threads needs no worry about the resources, while switching processes requires
- not independent and not protected against each other
	- threads can modify the shared part

![[Pasted image 20231019183031.png]]
![[Pasted image 20231019183043.png]]

`pthread_create(&thread_id, NULL, thread_function, (void *)i)`
`pthread_exit(0)`

Within a process, you can schedule mini jobs in a OS way by separating roles into threads, such as having a dispatcher thread and worker thread.

---
# Thread Implementation

- user level
	- implemented as a set of library functions
	- cannot be scheduled independently
	- each thread gets partial time quantum of a process
	- a system call by a thread blocks the entire set of threads of a process
	- less costly operations
- kernel level
	- implemented as system calls
	- can be scheduled directly by the OS
	- independent operation of threads in a single process
	- more expensive operations
- hybrid approach
	- combines the advantages of the above two
	- Solaris threads

---
# Warning

Threads access to the same data, so it is very hard to debug.

Thread Safe:
- it functions correctly during simultaneous execution by multiple threads