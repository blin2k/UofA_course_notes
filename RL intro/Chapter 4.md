# Policy Evaluation

- Policy evaluation
	- Determining the value function for a specific policy
	- First step
	- $\pi,P,\gamma\rightarrow v_\pi$
- Control
	- Finding a policy which maximizes the value function
	- Ultimate goal
	- $P,\gamma\rightarrow \pi_*$

# Dynamic Programming
Update Rule:
$v_{k+1}(s)\leftarrow \sum_a \pi(a|s)\sum_{s'}\sum_rP(s',r|s,a)[r+\gamma\cdot v_k(s')]$

Eventually, $v_{k}$ will converge to $v_\pi$
- Because $v_\pi$ is a unique solution to the Bellman Equation

# Iterative Policy Evaluation
$$\begin{align}
&\text{Input }\pi\text{, the policy to be evaluated}\\
&V\leftarrow\overset\rightarrow0,V'\leftarrow\overset\rightarrow0\\
&LOOP:\\
&\qquad \Delta\leftarrow0\\
&\qquad \text{Loop for each } s\in S:\\
&\qquad \qquad V'(s)\leftarrow\sum_a\pi(a|s)\sum_{s',r}P(s',r|s,a)[r+\gamma V(s')]\\
&\qquad \qquad \Delta\leftarrow max(\Delta,|V'(s)-V(s)|)\\
&\qquad V\leftarrow V'\\
&\text{until }\Delta<\theta\text{ (a small positive number)}\\
&\text{Output }V\approx v_\pi
\end{align}$$

---
# Policy Improvement

>[!Hint]
># Policy Improvement Theorem
>$\forall s\in S\qquad q_{\pi'}(s,\pi'(s))\ge q_\pi(s,\pi(s))\rightarrow \pi'\ge\pi$
>The new policy is a strict improvement over $\pi$ unless it is already optimal.$

$\forall s\in S\qquad \pi'(s)=\underset a{argmax}\sum_{s'}\sum_r P(s',r|s,a)[r+\gamma v_\pi(s')]$
Greedy

---
# Policy Iteration

Evaluation: $\pi_k\rightarrow v_{\pi_k}$
Improvement: $v_{\pi_k}\rightarrow \pi_{k+1}>\pi_k$

	Path preference renews the table, then the table infers a new path preference.

![[Pasted image 20231004165217.png]]

---
# Flexibility of the Policy Iteration Framework

## Generalized Policy Iteration

Unifies classical DP methods, value iteration, and asynchronous DP
### Value Iteration
![[Pasted image 20231004170145.png]]

- Avoiding full steps
	- Synchronous DP
		- one by one orderly
	- Asynchronous DP
		- randomly 
		- may repeat

---
# Efficiency of Dynamic Programming

- Monte Carlo Method
	- $v_\pi(s)\dot=\mathbb E_\pi[G_t|S_t=s]$
	- Expected (average) value of the return value
	- Lots randomness
	- Estimate each state independently
- Bootstrapping
	- $v_{k+1}(s)\leftarrow \sum_a\pi(a|s)\sum_{s'}\sum_rP(s',r|s,a)[r+\gamma v_k(s')]$
	- take advantage of the old results
- Brute-Force Search
	- Evaluate every possible policy one at a time

Compare to these naïve methods, DP is much faster in practice. 

## The Curse of Dimensionality

	The size of the state space grows exponentially as the number of relevant features increases.

	This is not an issue with DP, but inherent complexity of the problem.