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