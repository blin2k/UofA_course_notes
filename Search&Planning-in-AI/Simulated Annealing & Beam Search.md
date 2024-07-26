# Simulated Annealing
The iterations will turn into Hill Climbing from Random Walk.

- acceptance function
	- $P=min(1, e^{\frac{\beta}{T}\cdot h(c)-h(c'))}$
	- T: temperature parameter
		- $T_i=\frac{T_0}{1+\alpha\cdot i}$
		- large alpha will increase the process
	- $\beta$: pay more or less attention to h
	- P = 1 if the gap is positive
		- current one is better

At the beginning, T is high, so the heuristic gap will shrink and the term is less than 1. 
- accept every neighbor
- random walk
As the agent having more runs, T is getting lower and lower, the heuristic gap will be expanded. Thus, it will be rejected unless the gap is really close to 0.
- only accept close one
- hill climbing

![[Pasted image 20240417135318.png]]
![[Pasted image 20240417140712.png]]
The distribution
- positive gap
	- greater than 1
	- always chosen
- negative gap
	- since it's the power, resulting a small value
	- may or may not chosen

# Beam Search
From Hill Climbing to Breadth First Search

HC
- greedy on the best one

BFS
- check all of the neighbours

BS
- check the top k neighbours

![[Pasted image 20240417141856.png]]
