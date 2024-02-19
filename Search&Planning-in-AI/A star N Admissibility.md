In grid moving question, you can put the cost on a state by calculating the steps.

Using the open list and closed list, the agent will search the most close state first, which will create a cycle in 2D and sphere in 3D. The open list is used to pop the state out, and the closed list is used to collect all seen states.
![[Pasted image 20240202120103.png]]
This is a Dijkstra way. The inefficiency is that we know where the goal is so we don't need to explore the opposite way.

# Heuristic Function
Basically using math theory or your guts to find a solution.
- estimated the cost to go from a given state

Manhattan Distance
- if you move the opposite side to your goal, the distance will increase. You don't want that. So it could be an indicator.

$f(n)=g(n)+h(n)$
- this mixture function is not popping the node with the cheapest cost
	- cheap but in the opposite direction
- not the one most theoretically close to the goal
	- close but with a huge cost
- but a balance of them

How to break ties?
	Largest g-value or smallest h-value

## Notation
- $g^*(n)$
	- optimal cost between Si and n
- $h^*(n)$
	- optimal cost between n and Sg
	- may larger than h(n) when there is a wall
	- ![[Pasted image 20240202164813.png]]
		- you need 6 steps to get to the goal
		- you cannot make it with only 4 steps
- $f^*(n)$
	- optimal cost of a solution that goes through n

## Properties
- complete
	- it does not leave any states behind
- optimal
	- $A^*$ is optimal if: $g^*(n)+h(n)<P$ for a suboptimal solution P
		- $h(n)<P-g^*(n)$
			- not useful
	- $g^*(n)+h^*(n)<P\Rightarrow h^*(n)<P-g^*(n)$
		- because $h(n)\le h^*(n)$, it can lead to the optimal condition above
	- therefore, it is optimal if for all n: $h(n)\le h^*(n)$
		- admissible
		- sufficient but not necessary condition
- time complexity & memory complexity
	- you can't really know
	- worst case $O(b^d)$
	- best case $O(d)$
		- when h-values are consistent
			- $h(n)=h^*(n)$

worst case
	- $2^N$ expansions where N is the size of the state space
	- because it may reopen a tree when the f-value is update
- how to avoid re-expansions
	- when there is a transposition that cost c(n,x) from n to x
		- $g^*(n)+h(n)<P+h(x)$ is not useful
			- $h(n)-h(x)<P-g^*(x)$
		- $g^*(n)+c(n,x)<P\Rightarrow c(n,x)<P-g^*(n)$
			- because $h(n)-h(x)\le c(n,x)$, it can lead to the optimal condition above
			- ==it means the heuristic distance gap is smaller than the cost of moving==
				- notice that, in some cases, the agent chooses a path that has a lower gh sum but leading to a higher h. that's how re-expansion happens
			- otherwise, it costs too much to move such a short distance
		- if it is satisfied, for all n and x, then h is consistent
- observation: consistency implies in admissibility
	- $h(n)-h(x)\le c(n,x)$
	- if x is Sg
		- $h(n)-0\le h^*(n)$
		- the heuristic value of each node is its optimal

## Summary
A* is Dijkstra's with
- open sorted by f instead of g
- reopen nodes, if h is inconsistent