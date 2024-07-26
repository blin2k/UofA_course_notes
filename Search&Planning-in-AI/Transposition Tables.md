- BFS and Dijkstra's Algorithm do not suffer from transpositions
- IDDFS can suffer from transpositions
	- different path leading to the same position will be considered as different states
		- in a 4 by 7 map, there are 28 blocks
		- but there are multiple ways to get to the same block
		- assuming the agent starting from the bottom left  and trying to get to the top right, it requires 9 steps
		- that's 9 blocks on the map
		- but $4^9$ nodes because the agent can 1 action out of 4 on each block

We need a closed list to record the current path and delete it at the end.
- hash table used with IDDFS/IDA*
- limited memory
	- IDDFS doesn't need the table to recover path
	- Dijkstra's Algorithm need the whole table to recover solution path

Implementation
1. before expanding n, if n is not in the table, add n it and then expand it; ignore it if is in already seen
	1. if we went the long path first, the shortcut will be ignore
	2. ==the optimal is pruned==
2. add the g-value to the table; expand n if it is not in the table OR this path has a lower g-value
	1. know when to re-expand a node
	2. it ==works== but we can do better
		1. the memory of this path will be deleted when the depth is not deep enough
		2. since the closed list is wiped, by the order, a waste of re-expansion will happen again
			1. we want to learn from the information of the ==last research==
3. keep the closed list
	1. if a node has the same g-value as it on the list, it will be pruned
		1. which will prune the root first
4. add one more feature in the closed list: dimension
	1. for historical best g-values, if hits, expand it and update the dimension

Overall, there are three cases for expansions
- not in the table
	- $n\not\in TT$
- in the table but has a better value
	- $n\in TT\,\cap g(n)<TT[n].g$
- in the table, not having a better value but same as the best value over the previous searches
	- $n\in TT\,\cap g(n)=TT[n].g\,\cap d>TT[n].d$

