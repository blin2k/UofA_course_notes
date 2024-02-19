	One path at a time

- open list only
- last in first out
- same node may be added with different cost

Since we don't have a closed list, the agent may be trapped in a sub-tree.

How to make it COMPLETE and OPTIMAL?

Idea1
- bound the search by the optimal solution cost
	- once the current search has a higher cost, stop immediately
But how can we get the optimal solution cost beforehand?
- estimate
	- keep increasing the estimated cost until it hits
	- wrong path will be deleted from memory immediately

# Iterative-Deepening Depth-First Search
Def IDDFS(Si, Sg, T):
	B=0
	while not DFS(Si, Sg, T, B):
		B+=1

Def DFS(n, Sg, T, B):
	if n is Sg:
		return True
	if B<0:
		return False
	for neighbor in T(n):
		if DFS(neighbor, Sg, T, B-1)
			return True
	return False

---
IIDFS iteratively call DFS to check if there is a solution in the current estimated cost B. If not, we go deeper.

DFS first checks if we are starting from the goal and if the given depth is touching 0. If not, it will do the recursive part: for all neighbor nodes, call DFS with a shorter depth.

---
- complete
	- if there is a solution, we can find it
- complete+
	- if there is no solution, we are able to detect

C: BFS/Dijkstra/IDDFS
C+: BFS/Dijkstra

IDDFS cannot tell if there is a solution or not.

---
# Properties
- complete
	- but not complete+
- optimal
	- with respect to the number of actions
- memory complexity
	- $O(d)$
	- linear to the depth
- time complexity
	- children
		- $bd$
			- number of neighbors \* number of trees
				- each tree represents different depth
	- grand children
		- $b^2(d-1)$
			- each neighbor has the same amount of neighbors
			- the first tree has no grand children
	- grand grand children
		- $b^3(d-2)$
	- ending
		- $b^d$
	- by the definition, the highest dimension rules
		- $O(b^d)$

# Non-Unitary Cost

Set the bound to be the total cost.
