Factored States

In Classical Planning, it's all about path finding.
In Constraint Satisfaction, we don't care about paths.

# Map Coloring
The constraint is given by the edges

# Sudoku
![[Pasted image 20240418005000.png]]
domain
- what you can put in
variables
- where you can put in
constraints
- variables are not having the full domain
- form
	- scope, relation
		- $\{(X_{12},X_{13})\not=\}$
- type
	- unary
		- a kingdom cannot be green
	- binary
		- $\{(x,y),\not=\}$
	- global
		- $All_{Diff}\{X_{11},X_{12},X_{13},X_{14}\}$

# Arc Consistency
![[Pasted image 20240418011249.png]]
A variable is arc consistent if it satisfies its binary constraints.
- always binary because of the arc

![[Pasted image 20240418012740.png]]
You can trim the domain like this using the constraint

# AC3
![[Pasted image 20240418012940.png]]

Pop elements from Q and trim the domain for each variable

Once the domain of a pointed node changed due to an arc not between them, the domain of those nodes pointing to it changes as well. Thus, we need to put the arc back.
- put the element back to Q

def AC3(CSP):
	init Q with all arcs in the CSP
	while Q not empty:
		(x_i, x_j) = Q.pop()
		if revise((x_i, x_j)):
			for x_k in \{neighbors of x_i} \\ x_j:
				Q.add((x_k,x_i))

def revise(x_i, x_j):
	removed = false
	for d in domain(x_i):
		if there is no d' in domain of x_j that satisfies (x_i, x_j):
			remove d from domain(x_i)
			removed = true
	return removed

- revise() checks the domain of the first element. For each of them, if there is no element in the domain of the second element satisfies the constraint, remove this element from the domain of the first element
	- $O(d^2)$
	- a hidden for-loop in the outer for-loop
- AC3() keeps popping arcs. For each arc, do revise() to trim the domain of the first node. If it trims, all other nodes having an arc with it except the current arc should put back the arc between them.
	- $O(cd^3)$
	- the put-back increases a for-loop

# Search & Inference
- one value for each variable
	- find the solution
- at least one variable has an empty domain
	- prove no solution
- one or more values in each domain
	- search

Arc Consistent only proves that the domain between two nodes is compatible. But there may no have a solution since the arcs are linking each other.
![[Pasted image 20240418023154.png]]
- their probability is compatible when the arc is not confirmed
- when one arc is confirmed, there is no solutions

AC3 is used to shrink the domain so the problem will be easier but it's not used to generate the solution
# Backtracking
def Backtracking(A):
	if A is complete:
		return A
	var = select_var(A)
	for d in select_value(var, A):
		if d is not consistent with A:
			contintue
		{var = d} in A
		R = Backtracking(A)
		if R is not a failure:
			return R
	{var = None} in A
	return failure

- A is a whole state of all variables
- if A is filled, the solution is there
- otherwise, choose a variable and then try to assign a value in its domain
- if this value causes conflicts, skip it
- else, assign it and save it to A
- recursively keep going
- if the next node did not fail, return this back, it would be A
- otherwise, undo the assignment and return failure

# Search & Inference
Every time the search assigns a value to a variable, we try to simplify the problem with reasoning (AC3).

def Backtracking(A):
	if A is complete:
		return A
	var = select_var(A)
	for d in select_value(var, A):
		if d is not consistent with A:
			contintue
		{var = d} in A
		Ri = Inference(A)
		if Ri is not failure:
			R = Backtracking(A)
			if R is not a failure:
				return R
	{var = None} in A
	return failure

- using Ri to trim the domain of each variable in A
- if none of them is having failure, keep going

# Forward Checking
Ensures consistency to all arcs pointing to x_i once search assigns a value to x_i

![[Pasted image 20240418041752.png]]
Not able to see the conflict in this case
only in the next assignment
# Maintaining Arc Consistency
AC3 will go one step deeper
- the put back
	- this is the difference

# Which Variable to Try Next
- small domain size
	- small branching factor
	- maybe small subtree

# Minimum Remaining Value
After a partial assignment
- no solution
	- prove as quickly as possible
- has a solution
	- find a solution AQAP
		- minimize the branching factor make it easier

# How to Choose Variables at Root
- how to handle ties
	- select the variable with the largest number of connections
		- shrink the branching factor

# What About Values
- choose the unique one
- avoid the common one

If there is no solution, you are going to search all possibilities so it doesn't matter.

But in the case that there is a solution, choose the unique one so another node is more likely to have at least one value to put and thus go deeper and more likely to find a solution.

# Intelligent Backtracking


![[Pasted image 20240418094119.png]]
The previous layer is A, but it is not the one causing the current conflict.
- forward checking will avoid it

![[Pasted image 20240418100448.png]]
- AC3 and FC can't avoid this

![[Pasted image 20240418101404.png]]
After assigning D, it fails to assign C.
Backtrack to B, we need to assign another value for B.
Although B has no conflict with F, it has a conflict with D, and D is affected by F.
In the new conflict list of B, D is failed so there are A and F left.
- F is the closest one

In this way, it skips G.
- check the conflict instead of the decision

# Conflict-Direct Back Jumping
1. search with backtracking and reasoning
2. keep a list of conflicts as we run reasoning
3. when the partial assignment is inconsistent, then we are gonna backtrack to the closest variable x_j in the set of conflict(x_i), where x_i is the variable in which the variable in which the search detected the inconsistency

# Structure of the Problem
![[Pasted image 20240418102350.png]]
Try to run independently.
![[Pasted image 20240418102435.png]]
![[Pasted image 20240418102658.png]]
Recognize the structure and build a tree at the same time.
- assigning values as well because it is choosing variable

![[Pasted image 20240418102921.png]]
- not good when domain is not aligned

In arbitrary graph, we miss Arc Consistency
- go backward from leaf so you can check AC

# Tree Solver

def TreeSolver():
	topologicalSort()
	for j in range(n, 2):
		remove inconsistency of (parent(x_j), x_j)
	for i in range (1, n):
		x_i = v, where is consistent with its parent

$O(n)+O(nd^2)+O(n)$

You can also re-structure a non-tree graph into tree by cutting one node out.
- try all values to see if it works
