Goal: write a system that is able to solve any classical planning problem

- deterministic
- finite spaces

- fully observable
- static
	- environment will not change

- single agent
- pathfinding

Other settings can be compiled into classical planning.

Trade offs
- domain independent
	- quick results
		- just write down the problem
	- goal of AI
- domain dependent
	- more efficient
		- use domain strategy
	- more work

# Strips As a Planning Formalism

simple travel salesman problem
- no need to go back to the original city
![[Pasted image 20240418111422.png]]
propositions
- At(x)
- visited(x)
- connected(x,y)
	- (x,y) in {E,R,C}

initial state
- At(R), visited(R), c(E,R), c(R,C), c(R,E), c(C,R)
	- where the agent is
	- where he has been
	- where the current node connecting to

goal
- visited(x)
	- x in {E,R,C}

action
- drive(x,y)
	- pre
		- At(x), c(x,y)
	- add
		- At(y), visited(y)
	- del
		- At(x)

cost function
- c(drive(x,y))

state space
- ![[Pasted image 20240418111809.png]]
- ![[Pasted image 20240418111906.png]]

# Strips Planning Task

Tuple (P,A,c,I,G)
- P
	- a finite set of propositions
		- some of them may not exist in the graph but we list the probability anyway
		- e.g. c(E,C)
- A
	- finite set of actions
	- (pre, add, del)
- c
	- a cost function
	- A to $\mathbb R$
- I
	- initial state
	- in P
- G
	- goal
	- in P

# Strips State Space
Given $\pi$=(P,A,c,I,G), the state space $\theta_\pi$

$\pi$ induces define by tuple $\theta_\pi=(S,L,c,T,I,S^G)$
- S
	- set of states
	- all probabilities
- L
	- labels of the edges
	- the actions
- c
	- cost function
- T
	- transitions
	- ![[Pasted image 20240418113237.png]]
- I
	- initial state of $\pi$
- $S^G$
	- goal states

![[Pasted image 20240418113424.png]]

![[Pasted image 20240418113441.png]]

![[Pasted image 20240418113704.png]]
- yes or no
	- at city * 3
	- visited city * 3

![[Pasted image 20240418113817.png]]

# Planning Domain Definition Language

![[Pasted image 20240418114100.png]]

Domain file
- type of objects
- predicated
	- A is on the table
- action schema
![[Pasted image 20240418122501.png]]
![[Pasted image 20240418122621.png]]

Problem File
![[Pasted image 20240418122958.png]]

# Delete Relaxation
for each action a:
	a = (pre, add, del)

a^+ = (pre, add, None)
- relax the deletion
- once it is true, always true
- solution for relaxed plan for state s is a heuristic value for s
	- like PDB

![[Pasted image 20240418124753.png]]
- ignore the rule that we can only pick one block
	- pick one rule is defined by deletion
	- if you have no this block, you can't delete it
- it can be done in 3 moves

Approximate h^+
- h_max
	- cost of solving the problem is the most expensive subgoal
- h_add
	- cost of solving a problem is the sum of the cost of all subgoals
![[Pasted image 20240418125833.png]]
![[Pasted image 20240418130410.png]]
