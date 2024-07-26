Computer  program that generates a computer program that satisfies the user's intent.

# Search Space
Context-Free Grammar
![[Pasted image 20240417142731.png]]
- replace a variable with something else

Abstract Syntax Tree
![[Pasted image 20240417143420.png]]

# Searching with Simulated Annealing
- define an objective $J(p,D)$
	- p
		- program
	- D
		- set of input-output examples
	- $J(p,D)=\sum_{(x,y)\in D}[p(x)\not=y]$
		- the number of incorrect predicts
- accept function
	- $P=min\{1,e^{(J(p,D)-J(p',D))\frac{\beta}{T}}\}$

![[Pasted image 20240417150300.png]]
# Random Programs
![[Pasted image 20240417150431.png]]
Randomly choose one of the conditions in B
Randomly choose one of the values in S

Eventually, the if-then-else statement will hit the correct one.

# Problem
- can generate very long programs

# How to generate neighbors?
![[Pasted image 20240417150749.png]]
Generate the subtree randomly.