- BFS
	- expands the node that closest to the root of the tree
- Dijkstra's
	- expands the cheapest node in open

How?
- from FIFO to a priority queue
- will not stop immediately after hitting the goal
	- may not reaching the path with the lowest cost
	- when a better path shows up
		- renew the cost of goal in closed
			- also the parent
		- insert a new element to open
			- with new cost
- stop when the goal is popped

operations
- find and remove cheapest node from open (binary heap)
	- find: $O(1)$
	- remove and insert: $O(lgN)$
	- total: $O(lgN)$
- verify whether a state was seen in search (hash table)
	- includes checking for better paths
	- verify: $O(1)$

## Pseudo-code
Def Dijkstra(Si, Sg, T):
	open.insert(Si, 0)
	closed.add(Si)
	while (open is not empty):
		# in a priority queue, the popped on e will be the cheapest instead of FIFO
		n = open.pop() 
		if (n is Sg):
			return path
		for neighbor in T(n):
			if (neighbor is not in closed):
				# g(n) returns the cost of n
				# c(n, m) returns the cost to m from n
				open.insert(neighbor, g(n)+c(n, neighbor))
				closed.add(neighbor, g(n)+c(n, neighbor))
			if (neighbor is in closed) && (g(n)+c(n, neighbor) < closed\[neighbor\].g):
				closed\[neighbor].g = g(n) + c(n, neighbor)
				update parent pointer of neighbor in closed
				open.insert(neighbor, g(n)+c(n, neighbor))
	return failure

## Properties
- optimal
	- for the cost
- completeness
- time complexity
	- $O(b^{d+1})$
	- one more layer because we are not stop at the goal but at when the goal is popped 
- memory complexity
	- $O(b^{d+1})$