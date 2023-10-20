# Introduction

Computer systems
- hardware
	- electronic
	- mechanical
	- optical devices
- software
	- programs
		- user programs (Applications software)
		- operating system & utilities (Systems software)

Software allows a computer to store, manipulate, and retrieve information, and can engage in many other activities.

---
# Contemporary Hardware/Software Structure

Apps talk to utilities and some other hardware components. Then, the utilities will talk to the OS, and some device if needed.

OS can directly signal the app, or through the utilities.
![[Pasted image 20231019153825.png]]

---
# What is an OS?

==Resource manager== of both time and space.

Resources of a computer:
- processor
- main memory
- I/O devices

OS provides ==orderly and controlled== allocation and use of the resources, and ==hide the complexity== of the underlying hardware and give the user a better view of computer (Abstraction).

## Roles

- referee
	- communicate between users and apps
	- isolate different users and apps from each other
	- allocate resources among users and apps
- illusionist
	- each app appears to have the entire machine to itself
- glue
	- libraries
	- user interface widgets

---
# Study Purpose

- OS is one of the largest and most complicated software systems
- draws on lots of areas
	- software engineering
	- computer architecture
	- data structure
	- networks
	- algorithms
- the specific abstractions of an OS design, can affect an application's structure
- techniques used in an OS, can be applied to other areas
	- data structure design
	- concurrency
	- resource management
	- conflict resolution
	- security

---
# Interrupts

The OS gets control of the CPU when either an external or an internal event occurs.

External
- character typed on the console or keyboard
- completion of an I/O operation
- timer
	- avoiding infinite loops

Interrupts: the notification of an external event that occurs ==asynchronous== with the current activity of the processor.
	While doing one job, another job at a side signals the CPU for update.

## Handling

1. an interrupt occurs
2. jump to OS
3. execute the ISR
	1. handler section
4. return to the next line of where the interrupts occurs

All in one, the CPU suspends its current execution and services the interrupt first.

## More on Interrupts

- priority
	- when two interrupts occur simultaneously, one is serviced before the other
- nesting
	- an interrupt occurs while an interrupt is being serviced
- mask
	- when interruption of an interrupt handler is undesirable, other interrupts can be masked (inhibited) temporarily

---
# Traps

Internal
- system call
	- provide access to OS services
	- enter the OS and perform a privileged operation
	- indirectly change to supervisor mode
- error item
	- illegal instruction
	- addressing violation
	- divide by zero
- page fault

Trap: the notification of an internal event occurs while a program is executing, therefore is ==synchronous== with the current activity of the processor.
	The current job is facing some issues.

---
# I/O Techniques

Programmed I/O
- CPU transfers the data from/to the device buffers
- continuously check for completion (poll) while I/O in progress

Interrupt-driven I/O (low speed, character device)
- CPU goes on to some other work after issuing an I/O operation
- the device interrupts the CPU each time a byte or word arrives
- then the CPU handles the data transfer

Direct memory access (high speed, block device)
- CPU issues an I/O operation
	- specifying the device, memory location, and block size
- CPU free to do other works
	- DMA device will buffer a whole block of data
- DMA device interrupts CPU when completion

---
# Architectural Support

## Models of operation
- supervisor mode
	- all instructions
		- basic and privileged
- user mode
	- a subset of instruction
		- basic only
- hardware support for virtual machine

The design of two modes can protect the system from user programs, so no user programs can crash the OS. It also protects programs attack themselves or each other.
## I/O protection
- all I/O operations are privileged

## Memory protection
- base/limit registers (in early systems)
- memory management unit

## CPUT control
- timer
	- alarm clock
	- time-quantum
- context switch

---
# System Call Mechanism (Trap)

1. system call
2. switch to supervisor mode
	1. verify arguments
	2. jump to the privileged function table
	3. jump to the specific function
	4. return to the table
3. switch back to user mode
4. return to where the system call happens

---
# Kernel

Kernel = OS - Transient Components

Kernel is a portion of the OS remaining in main memory to provide services for critical operations, such as interrupt handling and resources management.