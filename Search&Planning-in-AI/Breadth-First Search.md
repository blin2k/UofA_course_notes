# Complete State Space
![[Pasted image 20240130225523.png]]
- the top are initial states
- the bottom are goal states

# Search Tree
- the root is the initial state
- expand the tree by looking at the neighbors and adding them as children nodes

Here are some inefficiency and how we fix that
- cycle
	- the parent became the child of its child
	- solution
		- parent pruning
- transposition
	- different paths go to the same node
	- solution
		- pick one of them
		- which?
			- the path with lower cost

You can keep a copy of a node in the tree, for example, allowing transposition. Because they are in different states.

expansion
- a state/node is expanded when we add its neighbors to the tree
generation
- a state/node is generated when its parent is expanded

# Uninformed Search Algorithms
- can't fit the graph in memory
- naturally leads to heuristic search

>[!notice]
>Bellman-Ford Algorithm
>- deal with negative cost
>- we won't see it in this course

Implicitly Defined State Space
- recursively generating states depending on move options
	- cherry-picking problem
		- options
			- Left / Right / Pick
		- ![[Pasted image 20240131001224.png]]

Properties we care
- complete
	- if the problem has a solution, then the algorithm will find it
- optimal
	- returns an optimal solution
- time complexity
	- the time that it takes to find a solution
- memory complexity
	- the amount of memory required to find a solution

---
# BFS
- break the graph into layers
	- the root is the first layer
	- the second layer will be nodes that the root can reach
	- keep expand if this is not a solution to the problem

How to implement BFS
- open list (queue/FIFO)
	- how
		- root gets in
		- root being popped
			- expand the root = the 2nd layer gets in
			- pop the 1st element in the 2nd layer
				- expand this element = part of the 3rd layer gets in
			- pop the next element in the layer
				- expand this element
			- ... = the 3rd layer is completed when the 2nd layer is popped entirely
	- organizes the search into layers
- closed list (hashtable)
	- remember all states seen in search
		- the open list implements parent pruning
			- will not remember the parent edge
			- cannot avoid transposition
	- avoids transpositions and cycles
	- recover the solution path
		- keeping track the parent

## Steps
1. add to open
2. add to closed
3. cancel and expand the oldest one in open
	1. expand to both open and closed
	2. if the generation is already in closed, stop generating it
4. go to 3
5. until we hit the goal state
	1. we don't have to add it to open or closed

## Pseudo-code

def BFS(Si, Sg, T):
	open.instert(Si)
	close.add(Si)
	while (open is not empty):
		n = open.pop()
		for neighbor in T(n):
			if (neighbor is Sg):
				return path
			elif (neighbor is not in closed):
				open.insert(neighbor)
				closed.add(neighbor)
	return failure

Properties:
- complete
	- all cases is handled
- optimal
	- for number of actions
		- by using a hash table tracing the parent
	- not for total cost
		- the shortest path may not be the one with the lowest cost
- time complexity
	- b is the branching factor
	- d is the solution depth
	- $\sum_{i=0}^d\,b^i=O(b^d)$
- memory complexity
	- $O(b^d)$