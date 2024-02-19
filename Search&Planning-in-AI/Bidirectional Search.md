- single directional search can grow exponentially with the solution depth
	- ![[Pasted image 20240201214755.png]]
- bidirectional search do the searches at the same time
	- ![[Pasted image 20240201214738.png]]
	- instead of $b^d$, we have $2\cdot b^{\frac b2}$

## Notation
- forward search
	- $g_F(n)$
		- Si to n
- backward search
	- $g_B(n')$
		- Sg to n'

## Data Structures
- two open lists
	- open-F, open-B
- two closed lists
	- closed-F, closed-B
- insert Si into open-F
- insert Sg into open-B

In every iteration:
- expand the cheapest node in either open lists
Solution path:
- for each state encountered in both searches
- not optimal

stopping condition:
1. state n is generated in both directions AND
2. $g_F(n)+g_B(n)\le g_{min_F}+g_{min_B}$
	1. solution cost <= lower bound on the solution cost if we continue searching
![[Pasted image 20240202000845.png]]
This is the first path, but it is not an optimal path.


![[Pasted image 20240202001141.png]]
This is an optimal path, but we cannot prove it. Thus, we are not going to stop here.

Then (n1, 2) is popped, the lower bound is still 2+3

Then (n8,2) is popped, the lower bound is 5+3, which is greater than the path we found. Now we can stop.

## Pseudo-code

Def Bi-Bs(Si, g, T):
	openF.insert(Si)
	openB.insert(g)
	closedF.add(Si)
	closedB.add(g)
	u = inf
	while (openF is not empty && openB is not empty):
		# epsilon is the lowest cost if you know it beforehand, it helps convergence
		if (u <= openF\[0].g + openB\[0].g + epsilon):
			return u
		if (openF\[0].g < openB\[0].g):
			n = openF.pop()
			# expanding
			for n' in T(n):
				# seen in the backward, it connects, check if it is better
				if (n' in closedB):
					u = min(u, g(n')+closedB\[n'].g)
				# not seen in backward, neither forward
				# put it in both forward lists
				if (n' is not in closedF):
					openF.insert(n')
					closedF.add(n')
				# seen in forward, it is a transposition, also a shortcut
				# update it for both forward lists
				if (n' in closedF && g(n')<closedF\[n'].g):
					closedF\[n'].g = g(n')
					update parent pointer for n'
					openF.insert(n')	
		else:
			# expand backward direction
	return failure	

---
# Memory Problem
- BFS
	- $O(b^d)$
- Dijkstra
	- $O(b^d)$
- Bi-Bs
	- $O(b^{b/2})$

Can we do better?
- Depth-First Search