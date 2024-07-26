For games like Go, it's hard to design heuristic function

Do tons of random games then assign the average value of all the terminals to the state

1. selection
	1. pop a node according to some selection algorithm
	2. tree policy
		1. which action to choose
		2. epsilon-greedy
	3. default policy
		4. for the simulation
		5. plays the game to the end with this policy
2. expansion
	1. find the neighbours
3. simulation
	1. average the value of all its terminals
4. backpropagation
	1. average and re-assign all actions along the decision chain

![[Pasted image 20240417214627.png]]

exploration vs. exploitation

# Minimize Regret
![[Pasted image 20240417220946.png]]
In a bandit problem, choose the bandit with the maximum expectation on the sum of all pulls

![[Pasted image 20240417223112.png]]
Subtract the regret
- expected the simulation sum

# Upper Confidence Bound
Every iteration, select the i that maximizes
$\bar x_i + \sqrt{\frac{2\cdot ln(n)}{n_i}}$

- average of the machine i
	- exploitation term
- n
	- total runs
	- grow fast
- n_i
	- runs on machine i
	- the machine with less pulling will have a large term
		- exploration term

# UCT
	UCB for Trees

Tree policy:
- choose the child j that maximizes $\bar x_j + c\cdot\sqrt{\frac{log(n)}{n_j}}$
- c
	- the exploration constant

UCT is different from UCB because we can't sample a child whenever we want. The child depends on the previous decisions.

for Max player:
- choose the action a that maximizes $Q(n,a)+c\cdot\sqrt{\frac{log(N(n))}{N(n,a)}}$
- Q
	- average utility of the action a on the node n
- N
	- the number of times choosing the node n
	- the number of times choosing the action a on node n

for Min player:
- minimize $Q(n,a)-c\cdot\sqrt{\frac{log(N(n))}{N(n,a)}}$
- subtract the exploration term