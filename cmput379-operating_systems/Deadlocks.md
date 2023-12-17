# Dining Philosophers
- philosophers sitting in a table
- sharing left and right utensils
- they need both to eat
- they are either eating or thinking

solution
- ![[Pasted image 20231214174728.png]]
	- if all of them pick up their left one, everybody waiting for the right one forever
- ![[Pasted image 20231214174934.png]]
- ![[Pasted image 20231214174948.png]]
	- one may keep losing the race condition
- what may work
	- allow at most four philosophers to contend for eating
	- allow philosophers to pick up both forks at once or none
	- asymmetry
		- have some philosophers grab the left fork first and then the right fork
		- have the others grab the right fork first and then the left fork
	- associate timestamps with hungry philosophers and use them to break contention

# What Is a Deadlock
	The permanent blocking of a set of processes that compete for system resourses, including database records or communication lines.

No efficient solution to deadlock problem in the general case.
- prevention by design is the best solution so far

All deadlocks involve conflicting resource needs by two or more processes.

resources
- reusable
	- can be safely used and is not depleted by that use
	- memory
- consumable
	- can be created and destroyed
	- signals

- preemptable
	- can be taken away from the process owning it with no ill effects
	- CPU
- non-preemptable
	- opposite to above
	- printer

Deadlocks occur when sharing ==reusable== and ==non-preemptable== resources.
- mutual exclusion
	- not sharing
	- cannot be disallowed
- hold and wait
	- wait while others holding
	- request all needed resources at one time, blocking until all requests can be granted simultaneously
- no preemption
	- not giving up until it is finished
	- release its unused resources and request them again
- circular wait
	- each process in the chain holds a resource requested by another
	- define a linear ordering of resource types
		- if a process has been allocated resources of type R, then it may ==subsequently== request only those resources of types following R in the order
	- ![[Pasted image 20231214183954.png]]

Cycle is a ==necessary condition== for a deadlock.
But when dealing with multiple unit resources - ==not sufficient==
- a knot must exist
	- a cycle with no non-cycle outgoing path from any involved node
	- ![[Pasted image 20231214220317.png]]

Strategies
- ignore
	- pretend there is no problem
- prevent
	- design a system
		- compile-time
		- statically
	- indirect
		- prevent one of the conditions
	- direct
		- prevent the circular wait condition
- avoid
	- dynamically checking whether the request will potentially lead to a deadlock or not
		- run-time
		- dynamically
- detect
	- let the deadlock occur and take some action to recover
		- run-time
		- dynamically


# Dijkstra's Banker's Algorithm

- n processes Pi
- m resources Rj
- avail_j
	- units of each resources

- max_ij
	- n x m matrix
	- the value of entry_ij is units request from Rj to Pi
- hold_ij
	- units hold by Pi from Rj
- need_ij
	- remaining need by Pi from Rj

- need = max - hold

When Pi request, post it in vector req_j
1. if req_j > need_i
	- error -> abort
2. if req_j > avail_j
	- not enough -> goto 1 and loop waiting
3. provisional allocation
	- avail_j -= req_j
	- hold_ij += req_j
	- need_ij -= req_j
	- if isSafe()
		- grant resource
	- else
		- cancel allocation
		- goto 1 and loop waiting

isSafe()
- work_j = avail_j for all j; finish_i = false for all i
- find
	- finish_i =false; need_ij <= work_j for all j
		- in process and resources are enough
	- if cannot found, goto 4
- work_j += hold_ij; finish_i = true; goto 2
	- pretend it finish and release resources
	- find next process
- if finish_i = ture for all i
	- return ture
- else return false


- very safe
	- need_i <= avail_i for all Pi
		- enough for one more chance
- safe
	- need_i > avail_i for some Pi
		- some enough but some does not
	- at least one correct order they may complete their use of resources
- unsafe (deadlock inevitable)
	- need_i > avail_i for some Pi
	- some processes cannot complete successfully
- deadlock
	- need_i > avail_i for all Pi
		- all ready blocked

# Recovering From Detecting Deadlocks
- preemption
	- temporarily take a resource away from its current owner and give it to another
- rollback
	- arrange to have processes checkpointed periodically
- termination
	- trivially break the deadlock by killing one or more processes