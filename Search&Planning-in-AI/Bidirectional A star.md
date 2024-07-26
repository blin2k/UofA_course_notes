![[Pasted image 20240229224858.png]]
![[Pasted image 20240229225142.png]]
Keep popping ==the cheapest among two lists== until a hit
- $g_F(A)+g_B(A)=5\le f_{min}$
	- the total g-value is less or equal to the f-value
- in this case, the forward list did not move as many as the backward one
	- not splitting equally
![[Pasted image 20240229230122.png]]
How we define "meet at the middle"
- no search expands states whose cost > 0.5 C* 

![[Pasted image 20240229230613.png]]
use the g-value only
- Dijkstra

# How to Meet in the Middle
$P_F(n)=max\left(f(n),2\cdot g(n)\right)$
- A* knows where to go but not splitting the work
- Dijkstra splits the work but may waste time on wrong path

The 2nd term sets a constraint on the f-value picking schema by setting more weight on the g-value
- encourage to go far

![[Pasted image 20240301073213.png]]
Show that $S_{k+1}$ will not be expanded in forward search
![[Pasted image 20240301073540.png]]
![[Pasted image 20240301073722.png]]
![[Pasted image 20240301073844.png]]
![[Pasted image 20240301074109.png]]![[Pasted image 20240301074308.png]]
If the node crossed the line
- forward
	- using the 2nd term
	- too expensive
- backward
	- using the 1st term
	- too expensive

# Pseudo-code
Def MM(Si, Sg, T):
	openF.insert(Si)
	openB.insert(Sg)
	closedF.insert(Sg)
	closedB.insert(Si)
	u = inf
	while (not openF.empty()) && (not openB.empty()):
		if $stopping_condition:
			return u
		if openF\[0] < openB\[0]:
			n = openF.pop()
			for n' in T(n):
				# meet
				if n' in closedB:
					u = min(u, closedB\[n'].g + g(n'))
				# not meet, seen, and found a shortcut
				if (n' in closedF) && (g(n') < closedF\[n'].g):
					openF.insert(n')
					update parent of n' and costs in closedF
				if n' is not in closedF:
					openF.insert(n')
					closedF.add(n')
				else:
					backward_expansion

# Stopping Condition
![[Pasted image 20240301082155.png]]
- the first term
	- original in bidirectional search
	- total cost is smaller or equal to the smallest g-sum of both sides
- 2nd and 3rd term
	- f-value is the theoretical cost
- 4th term
	- also a lower bound

All 4 conditions are ==lower bounds==

---

Near-Optimal Bidirectional Search