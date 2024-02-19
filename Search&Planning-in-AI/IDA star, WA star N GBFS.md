![[Pasted image 20240209124530.png]]
- s-x is a suboptimal path
- s-n-x is an optimal path

To avoid re-expansion, we want the agent go to n before it go to x.
- the agent chooses path by the open list
- from s, n should have a smaller value than x
	- $g^*(n)+h(n)<P+h(x)$
	- $h(n)-h(x)<P-g^*(n)$

Since we know s-n-x is an optimal path,
- $g^*(n)+c(n,x)<P$
	- $c(n,x)<P-g^*(n)$
	- c is the best cost
	- the right hand side must have some extra values

Combining these two,
- $h(n)-h(x)\le c(n,x)<P-g^*(n)$

- if n is closer to the goal than x
	- $h(n)-h(x)<0<c(n,x)$
	- choose n
- else if n is not closer to the goal, but the the distance between n and x is shorter than the best cost between n and x
	- $0<h(n)-h(x)<c(n,x)$
	- choose n
- else
	- choose x

==This is called Consistency==

If the agent move from A to B, the distance it moved towards the goal is less than the current best cost of the move.

---
# Other Heuristic Search Algorithms

The heuristic version of Dijkstra is A\*.
What we gonna do next is to find the heuristic algorithms of IDDFS and BFS
- IDA\*

Also we are interested in Bounded Suboptimal Solutions
- converge fast
- WA\*
- WIDA\*

And Suboptimal Solutions
- Greedy Best-first Search

---
# IDA\*
f(n) is the estimated cost of solution going through n

- use h(Si) as the initial bound
	- we don't need to start from 0 because the heuristic value implies the distance
- if h is admissible
	- $h(n)\le c^*(n)$
	- $f(n)\le c^*(n)$

The bound B will increase until a hit. So depth smaller than B has no solutions, and the current B is the upper bound of the initial bound h(Si)=C\*(Si).

If a node n has a f-value larger than B, that means, the estimated cost from this node to the goal is larger than the the initial cost h(Si). Thus we can prune that node since we know if the agent touched this node, even the best result will larger than the bound.

![[Pasted image 20240215233628.png]]
In this example, 
1. heuristic defines f(Si) = h(Si) = 4
2. the agent chooses neighbor in order
	1. the top right
3. the agent determines if left is a nice move
	1. f(n11) = f(n11) + g(n12, n11) = 5 + 1 = 6
	2. the current bound is 4 > 6
	3. prune this child
4. the agent determines down
	1. f(n22) = f(n22) + g(n12, n22) = 3 + 1 = 4
	2. within the bound
	3. expand
5. same thing repeats, the agent always expand down child

![[Pasted image 20240215235425.png]]
With a wall, the agent at n32 will:
1. see n33
	1. prune
2. see n22
3. see n23
	1. prune
4. see n21
5. see n23
	1. prune
6. see n12
	1. prune
7. no solution in B=4
	1. assign the cheapest pruned value to B
		1. B = 6
8. the agent will go the left path with all 6s
![[Pasted image 20240216001026.png]]
# Summary
- B=f(Si)=h(Si)
- prune n if f(n)>B
- set B to the smallest f-value pruned in the previous iteration

# Properties
- optimal
	- if h is admissible
	- sufficient but not necessary
- complete
- memory complexity
	- $O(d)$
- time complexity
	- ?

# WA\* & WIDA\*
	Weighted

Multiply h(n) by w>1
- f(n) = g(n) + w\*h(n)

By weighting the heuristic value heavier, tie situation is less likely to happen. The heuristic choice will have a cheaper value.

If heuristic is admissible, then WIDA* and A* find bounded suboptimal solutions:
	solution cost <= wc*
![[Pasted image 20240216011501.png]]
# Best-first Search
	Only care about heuristic