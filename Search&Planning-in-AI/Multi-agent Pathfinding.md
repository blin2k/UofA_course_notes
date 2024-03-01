# MAPF
- two agents cannot stay in the same cell at the same time

Using graph(V,E) but not representing the state space, and a set of K agents.
- represents the map structure
- each node is a cell
- each edge is a connection
Each agent has a start and target nodes.

How many states in the state space?
- $P_{cell}^{agent}=\frac{cell!}{(cell-agent)!}$
- much larger than the graph

---
- task
	- find a path for each agent
- constraint
	- paths cannot overlap
		- two agent cannot stay in the same cell at the same time
- objective
	- several options, depending on the problem domain
		- make span
			- minimize the most expansive task
		- sum of the costs
			- minimize the sum of the cost of all path

The search tree is also created with parents and children
- children are the states that could happen next
	- each agent takes an action
	- ![[Pasted image 20240216115907.png]]

## Heuristic Functions
	If we want to use A*, then we need a heuristic function.

Makespan
- max of estimated cost-to-go of all agents
	- ignores agents/walls
	- estimates
	- take the maximum
	- ![[Pasted image 20240216120500.png]]

- options
	- max of Manhattan Distance of all agents
	- max of the optimal solution cost while ignoring all the other agents
		- each of the optimal solution cost requires A*
		- that's time consuming

Sum of Costs
- sum of length of all paths while ignoring the other agents
	- in the last example, we use max()
	- here, we use sum()
		- h(n) = 7+4+7+6=24
- same two options
	- o2 tend to be better
	- o1 tent to be faster

For A actions and K agents
- there are $A^K$ states
	- each agent choose 1 action
- not even A* with h* will find solutions to some of these problems

Multi-Agent Path Finding is computationally hard (NP-hard)
- we won't be able to solve all problems
- but we can solve some, with clever tricks 

# Cooperative A*
Let one of the agent find its path using A*, then let the time steps of this path be the constrain of other agents.

## Pseudocode
pi = {}
for each agent a:
	P = find a path for a while ignoring other agents and satisfying the constraints
	pi.add(P)
	for each step in P:
		block(location, time) of the step
return pi

## Properties
- not complete
	- A* tells the agent go to the target directly, what if there is a one-way path and the first agent is blocked by other one?
		- in this case, the algorithm cannot give the solution
	- what is the solution?
		- the first agent hides somewhere so another one can pass the path and not blocking the path anymore
- not optimal
	- the order of agents will affect the solution
		- an agent's path may block all targets for one round
		- this can be avoid by adjust the order

# Conflict-Based Search
	When there is a conflict, instead of the later agent needs to wait, we consider both cases: the former one waits and the later one waits.

Main idea: Try all possible fixes to the constrains we find along the way.

1. plan for each agent separately
2. if paths for i and j conflict
	1. constrain i to avoid conflict
	2. constrain j to avoid conflict

![[Pasted image 20240216162725.png]]
	B is the one-way conflict point

The two children shown above is hitting the goal, so the tree stops here.

## CBS Tree
Node
- constrains
- solution paths
- start and goal locations for each agent
- cost of node

Goal test:
- check for conflicts in the solution paths

Successor function:
- find a conflict
- for a pair of agents(a1,a2) in the conflict
	- create a child where a1 cannot use the cell at t from the conflict
	- another child for a2
	- run A* for each child

![[Pasted image 20240216180337.png]]
The first approach
- each node represents a conflict
	- implies that the rest one is having higher priority

The second approach
- implies there is one having higher priority
- the children are two agents having a conflict
	- the children of them are other conflict pairs, plus itself
	- duplication exists but we can prune it

![[Pasted image 20240216181251.png]]
- the chosen one stay the same in the solution list
- the other one puts the node in conflict list, then runs A* with this conflict 

- the constraints to a parent is a subset of the constraints to its children.
- the cost for a node is the sum of costs of all agents
- cost will not get cheaper, but might stay the same

# Pseudo-code
def CBS(start):
	# run A* for all agents
	start.compute_cost()
	if start.cost is inf:
		return "no solution"
	open = \[]
	open.push(start)
	while open is not empty:
		n = open.pop()
		if n is a solution:
			# paths are stored when computing the cost
			return n.paths, n.cost
		for n' in T(n):
			n'.compute_cost()
			if n'.cost is not inf:
				open.push(n')
	return "no solution"
