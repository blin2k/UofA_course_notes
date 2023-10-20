# Concurrency

Overlap computation with I/O, improving the performance.
- hardware parallelism
	- CPU computing
	- one or more I/O devices are running at the same time
- pseudo parallelism
	- rapid switching back and forth of the CPU among processes
	- pretending that those processes run concurrently
- real parallelism
	- can only be achieved by multiple CPUs

In a multi-programming environment, processes executing concurrently are either ==competing== for the CPU and other global resources, or ==cooperating== with each other for sharing some resources.
- avoid competing
	- carefully allocate resources
	- properly isolate processes from each other
- help cooperating
	- provide mechanisms to share resources
	- allow processes to properly interact with each other

Cooperation
- implicit sharing
- explicit communication

Process:
- competing
	- cannot affect the execution of each other
	- compete for devices and other resources
	- do not intend to work together
	- unaware of one another
	- example
		- independent processes
	- properties
		- deterministic
		- reproducible
		- can stop and restart without side effects
		- can proceed at arbitrary rate
- cooperating
	- aware of each other
	- directly or indirectly work together
	- may affect the execution of each other
	- example
		- transaction processes in airline reservations
	- properties
		- share or exchange something
		- non-deterministic
			- you do not know how would they affect the execution of each other
		- may be irreproducible
			- may not get the same result if you run it again
		- subject to race conditions
			- the fast one can change the global variable


## Why Cooperation?
- share some resources
	- one checking account file, many tellers
- do things faster
	- read next block while processing current one
	- divide jobs into smaller pieces and execute then concurrently
- construct systems in modular fashion

## Potential Problem

Race condition
	situation where two or more processes access shared data concurrently, and correctness depends on specific interleaving of operations.

Mutual exclusion
	a mechanism to ensure that only one process is doing certain things at one time, thus avoid data inconsistency. All others should be prevented from modifying shared data.

Critical section
	a section of code, or a collection of operations, in which only one process may be executing at a given time and which we want to make "sort of" atomic.
- atomic
	- either an operation happens in its entirety or NOT at all

# Solutions
## attempt 1
```
if (noMilk){
	if (noNote){
		leave a note;
		buy milk;
		remove note;
	}
}
```

the first three lines are not atomic

## attempt 2
```
leave noteA
if (noNoteB){
	if (noMilk){
		buy milk;
	}
}
remove noteA
```

```
leave noteB
if (noNoteA){
	if (noMilk){
		buy milk;
	}
}
remove noteB
```

After A and B leave notes, A sees note B, trying to remove note A but not complete yet, B sees note A. Then A removes note A, and B also removes note B. Eventually no one gets the milk.

## attempt 3
```
leave noteA
if (noNoteB){
	if (noMilk){
		buy milk;
	}
}
remove noteA
```

```
leave noteB
while (noNoteA);

if (noMilk){
	buy milk;
}
remove noteB
```

Asymmetric solution works, but too complicated. And it would be even more complicated if extended to many processes.

---
# Fundamental Requirements

1. mutual exclusion
	1. no two processes will simultaneously be inside the same critical section
2. progress
	1. a process wishing to enter its CS will eventually do so in finite time
3. fault tolerance
	1. processes failing outside their CS should not interfere with others accessing the CS
4. no assumptions
	1. should be made out relative speeds or the number of processors
	2. must handle all interleaving
5. efficiency
	1. a process will remain inside its CS for a short time only, without blocking

---
## ME attempt 1
```
while (1){
	while (proc == B){
		CS;
		proc == B;
	}
}
```

```
while (1){
	while (proc == A){
		CS;
		proc == A;
	}
}
```

Violate rule progress
	One of them will never get into its CS.

## ME attempt 2

```
while (1){
	while (pBinside);
 
	pAinside = true;
	CS
	pAinside = false;
}
```

```
while (1){
	while (pAinside);
 
	pBinside = true;
	CS
	pBinside = false;
}
```

Violate rule mutual exclusion
	A passes the while loop and not yet setting pAinside to be true, B can also passes the while loop. Then both of them can be in the CS at the same time.

## ME attempt 3

```
while (1){
	pAtrying = true;
	while (pBtring);

	CS
	pAtring = false;
}
```

```
while (1){
	pBtrying = true;
	while (pAtring);

	CS
	pBtring = false;
}
```

Violate rule progress
	A starts to try but not yet touch the while loop, B also starts trying. Both of them stuck in the while loop forever.

---
## Dekker's
```
while (1){
	pAtrying = true;
	while (pBtrying){
		if (turn == B){
			pAtrying = false;
			while (turn == B);

			pAtrying = true;
		}
	CS
	turn = B;
	pAtrying = false;
	}
}
```

```
while (1){
	pBtrying = true;
	while (pAtrying){
		if (turn == A){
			pBtrying = false;
			while (turn == A);

			pBtrying = true;
		}
	CS
	turn = A;
	pBtrying = false;
	}
}
```

Before the while loop, if B is not trying, A straight up to CS. It does not affect B getting into its CS.

If both of them are trying, the one is not in the turn will stop trying and starting to wait until the one in the turn finishes CS and change the turn.

## Peterson's

```
while (1){
	pAtrying = true;
	turn = B;
	while (pBtrying && turn==B);

	CS
	pAtrying = false;
}
```

```
while (1){
	pBtrying = true;
	turn = A;
	while (pAtrying && turn==A);

	CS
	pBtrying = false;
}
```

If both of them are trying, the one in the turn will go to CS while the other one waiting. After finishing CS, the one in turn will stop trying and then the waiting one could get in.

---

Both Dekker's and Peterson's are correct, but only work for two processes.

---
## Bakery

```
# int i = process #
boolean choosing[n];
int number[n];

while(1){
	choosing[i] = true;
	number[i] = max(number[0],...,number[n-1]) + 1;
	choosing[i] = false;
	for(j=0; j<n; j++){
		while(choosing[j]);

		while(number[j] != 0 && (number[j] < number[i]));
	}
	CS
	number[i] = 0;
}
```

1. telling everyone that I am getting my number
2. get the number, which is larger than the largest one
3. telling everyone that I am done with getting number
4. check everyone
	1. if this one is choosing a number
		1. wait
	2. have a number
		1. not pass CS yet and have a smaller number
			1. wait
		2. everyone still in line have larger numbers
			1. go to 5
5. CS
6. telling everyone that I have pass my CS

---
# Simple-Minded Alternative
```
while(1){
	disableInterrupts();
	CS
	enableInterrupts();
}
```

With this hardware support, the instruction is guaranteed atomic. Only the one disabled interrupts can get in the CS, others will be interrupted.

However, no OS allows user access to privileged instructions. And there is only one CS active at a time for the whole system! Even other irrelevant process will be interrupted.

---
## Hardware Support

Many CPU today provide hardware instructions to read, modify, and store a word atomically.
- TAS
	- test and set
	- Motorola 68K
- CAS
	- compare and swap
	- IBM 370
- XCHG
	- exchange
	- x86
- LL/SC
	- MIPS

They all finish within one execution cycle.

---
## Another Alternative

```
boolean TAS(int *flag){
	boolean result = *flag;
	*flag = true;
	return result;
}

while(1){
	while(TAS(&guard));

	CS
	guard = false
}
```

`TAS()` returns the value of the argument, and set the argument to be a Boolean true.

When there is no guards, `TAS()` returns false so the process can get in CS, at the same time, it tells everyone that it is guarded now. Unguard after CS.

---
# Semaphores

	A synchronization variable (guard) that takes on non-negative integer values with only two atomic operation.

```
Proberen(semaphore){
	while(semaphore == 0);

	semaphore--;
}

Verhogen(semaphore){
	semaphore++;
}
```

```
P(OKtoBuyMilk);
if (noMilk){
	buy milk;
}
V(OKtoBuyMilk);
```
OKtoBuyMilk initially be set to 1.

The first one will reduce OBM to 0 and get into CS. Before it exits CS and increases OBM, others can only wait.

## Properties

- simple
- work with many processes
	- single resource serialization
- can have many different CS with different semaphores
- each CS has unique access semaphore
- can permit multiple processes into the CS at once, if desirable
	- multiple (identical) resources

- unstructured
- do not support data abstraction

## Possible Uses

- mutual exclusion
	- initialize semaphore to 1
- synchronization of cooperating processes
	- initialize semaphore to 0
	- no one gets in
- managing multiple instances of a resource
	- initialize semaphore to the number of instances
	- can get in until semaphore is 0

## Type of Semaphores

- binary
	- integer 0/1
- counting
	- integer between 0 and arbitrary large number
	- might represent the number of units of the CS that are available
	- general semaphore

## Implementation

No existing hardware implements P and V directly. So it must be built up using some other elementary synchronization primitives provided by hardware.

- uni-processor
	- disable interrupts
	- use hardware support
- multi-processor
	- turn off access of all other processors
		- not practical
	- use hardware support for atomic operation

### binary-busy wait
```
wait(int &s){
	while(TAS(s));

	return;
}

free(int &s){
	s = false;
	return;
}
```

Spinlock
- the process spins while waiting for the lock
- potential indefinite postponement
- low efficiency (busy waiting)

### non-busy wait
```
typedef struct{
	int value;
	list *waitQ;
}semaphore;

P(semaphore *s){
	s->value--;
	if (s-value < 0){
		addQ(pr, s->waitQ);
		block(pr);
	}
	return;
}

V(semaphore *s){
	s->value++;
	if (s->value <= 0){
		pr = removeQ(s->waitQ);
		wakeup(pr);
	}
	return;
}
```

If there is no available place, set the current process to the waiting queue and block it for a while.

After an increment, if there is still extra available resource, just arrange some one in the queue to be the next.

### Read & Write

	Allowing one writer at a time, and many readers.

```writer
P(wrt);
write...
V(wrt);
```

```reader
P(mutex);
readcount++;
if (readcount == 1){
	P(wrt);
}
V(mutex);

read...

P(mutex);
readcount--;
if (readcount == 0){
	V(wrt);
}
V(mutex);
```

For all the readers, only one reader can sign up for reading at a time. 
After the announce, if the reader is the only one, either the writer performs writing or the reader performs reading. Other readers are free to sign up now.
Same, only one reader can sign out at a time. If the reader is the only reader, the writer is free to write.

---
# Monitors

	A high level abstraction that combines the following
- shared data
- operations on the data
- synchronization with condition variables

Mutual exclusion is not sufficient for concurrent programming. An additional way to block processes is also need (when resource busy or buffer full).

Monitors use condition variables (binary semaphores) to provide user-tailored synchronization and manage each with a separate condition queue.

The only operation available on these variables are `wait()` and `signal(0`

## Semantics

- only one process executes in the monitor at any point in time
	- mutual exclusion
- access to data exclusively through a set of procedures (methods)
	- security
- processes wait at the entry point, or through specific synchronization calls
	- related to condition variables
- for a condition variable $x$, the following are defined
	- `x.wait()`
	- `x.signal()`

## Other High Level Primitives

- critical regions
- barriers
- conditional critical regions
- event counts
- sequencers
- path expressions
- serializers

They are semantically equivalent 
Any one can be built using the others
Essentially provided by the systems software (OS or language compilers) as programming tools

---
# Transactions

	Large atomic operation accessing a shared database

Transaction terminated by
- commit
	- successful termination
- abort
	- unsuccessful termination
	- might have changed data it has accessed
	- need to roll back the transaction
		- log-based recovery
			- keep track of all changes to a record
		- checkpoints
			- snapshot of the state

---
# Serializability

	When the outcome of the concurrent execution of atomic transactions should be equivalent to the sequential execution of the same transactions in an arbitrary order.

![[Pasted image 20231020000714.png]]

## Problems

- write/write
	- overwriting uncommitted data
	- blind ++/--
		- same change occurs twice
- write/read
	- reading modified, but uncommitted, data
	- one transaction aborts, but have read by another transaction
- read/write
	- unrepeatable reads
	- one transaction reads before another transaction commits
	- re-read will get a different value
---
# Concurrency & Serializability

Associate each data item with a lock
- must possess lock to access the data item
	- lock mode
		- shared
			- allows reading only, others can also lock as shared
			- prevent r/w conflicts
		- exclusive
			- allows reading and writing, others cannot hold the lock
			- prevent w/r and w/w conflicts
- locks are not enough
	- must know when to release
	- simplistic approach
		- obtain all at the beginning and release all at the end
	- better approach
		- two phase locking
			- first phase
				- growing phase
					- may obtain but not release
			- second phase
				- shrink phase
					- may release but not obtain

---
# Problems With synch Primitives

The most important deficiency of the synchronization primitives discussed so far is, 
they were all designed on one or more CPUs accessing a common memory.

Hence, these primitives are not applicable to distributed systems.

Solution: Message passing