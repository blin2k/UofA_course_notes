![[Pasted image 20240301090418.png]]
permutation

![[Pasted image 20240301090610.png]]
no queen attaching others

![[Pasted image 20240301090824.png]]

We just need the configuration of the solution.

![[Pasted image 20240301091620.png]]![[Pasted image 20240301091649.png]]

- pure search
	- find a solution
		- valued as 1
		- while non-solutions are valued as 0
	- maximize the function
- pure optimization
	- find the optimized solution among all solutions

# Hill Climbing
- random init
- choose the best neighbor and replace the current one
- until the best neighbor is as good as the current one
	- local optimal

# Sideways Moves
- not stop but keep going when the best neighbor is as good as the current one
- problems
	- does not guarantee to find the global optimum
	- might stuck in an infinite loop
		- bound the number of sideway moves

# Stochastic Hill Climbing
- not greedy on the lowest heuristic value
- define a probability distribution
	- $\frac{h_i}{\sum h}$
- might go back sometimes

# Random Restarts
- keep running Stochastic Hill Climbing with different starting point
- greedy on the results of all those runs


# Random Walks
- randomly choose the next candidate
- ignore h
	- losing guidance
	- no longer get stuck in local optima

- asymptotically compute and optimal
	- very slow

It can be combined with HC
- be greedy when not trapped
- do random walk when it is trapped