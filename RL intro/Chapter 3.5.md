# Policies

## Deterministic Policy Notation
- $\pi(s)=a$
- mapping States to Actions

## Stochastic Policy Notation
- $\pi(a|s)$
	- $\underset{a\in\mathcal A(s)}\sum \pi(a|s)=1$
	- $\pi(a|s)\ge 0$

- Under a certain policy, the agent would have preference over all actions. Thus, a ==probability distribution== formed.
- only depend on the current state

---
# Value Functions

## State-Value Function
- $v(s)\dot=\mathbb E_\pi[G_t|S_t=s]$
	- $G_t=\sum^{\infty}_{k=0}\gamma^kR_{t+k+1}$
	- Under a certain policy, given the current state, the expected return value 

## Action-Value Functions
- $q_\pi(s,a)\dot=\mathbb E_\pi[G_t|S_t=s,A_t=a]$
	- Under a certain policy, specifying the current state and action taken, the expected return value
	- Benefit
		- Allowing an agent to query the quality of its current situation instead of waiting to observe the long-term outcome.
			- e.g. In chess games, the agent doesn't need to wait for the reward which takes an entire game. Instead, it can valuate every action it can take under the current state. 
	- Shortcoming
		- The return is not immediately available
		- The return may be random due to stochasticity in both the policy and environment dynamics
  
  ---
# Bellman Equation Derivation

## State-Value Bellman Equation
[[Chapter 3.5#State-Value Function]]
$$\begin{align}
v_\pi(s)&\dot=\mathbb E_\pi[G_t|S_t=s]\\
&=\mathbb E_\pi[R_{t+1}+\gamma G_{t+1}|S_t=s]\\
&=\sum_a\pi(a|s)\sum_{s'}\sum_r p(s',r|s,a)[r+\gamma\mathbb E_\pi[G_{t+1}|S_{t+1}=s']]\\
&\text{Since the current state is known, the first sum list all actions and iteratively spesifies one action. }\\
&\text{The next two sums list the probability of next state and reward, under the current state and one }\\
&\text{of the actions. The last part represents the next return value.}\\\\
&\text{Notice that the first sum covers the rest instead of just the }\pi.\\
&=\sum_a\pi(a|s)\sum_{s'}\sum_r p(s',r|s,a)[r+\gamma\cdot v_\pi(s')]\\
\\\\
q_\pi(s,a)&=\mathbb E_\pi[G_t|S_t=s, A_t=a]\\
&=\sum_{s'}\sum_r p(s',r|s,a)[r+\gamma\mathbb E_\pi[G_{t+1}|S_{t+1}=s']]\\
&=\sum_{s'}\sum_r p(s',r|s,a)[r+\gamma\sum_{a'}\pi(a'|s')\mathbb E_\pi[G_{t+1}|S_{t+1}=s',A_{t+1}=a']\\
&\text{Since the action taken is known, we can expand the expected value as, the sum of,  the}\\
&\text{probability of the next action times the the next expected reward given the next state }\\
&\text{and action.}
\end{align}$$

### Why Bellman Equation?
![[Pasted image 20231004102252.png]]
![[Pasted image 20231004102304.png]]

- You can use the Bellman Equations to solve for a value function by writing ==a system of linear equations== 

---
# Optimal Policies

$\pi_1\ge\pi_2$ iff $\forall s\in S\qquad v_{\pi_1}(s)\ge v_{\pi_2}(s)$

There is always at least one optimal policy $\pi_*$
1. $\pi_*$ exists
2. $\pi_1$ intersects with $\pi_2$
	- Combine them by taking the actions according to whichever of policy has the highest value
	- Necessarily have a better value in every state

---
# Optimal Value Function

$v_*=v_{\pi_*}(s)\dot=\mathbb E_{\pi_*}[G_t|S_t=s]=\forall s\in S\qquad \underset\pi{max}\quad v_\pi(s)$
$q_*=\forall s\in S,a\in A\qquad \underset\pi{max}\quad q_\pi(s,a)$

# Bellman Optimality Equation for $v_*$ and $q_*$

We don't need the expected value anymore, because we knew which is the best action to take under the optimal policy.
- $v_*=\underset a{max}\sum_{s'}\sum_r P(s',r|s,a)[r+\gamma v_*(s')]$
- $q_*=\sum_{s'}\sum_r p(s',r|s,a)[r+\gamma\cdot \underset {a'}{max}\quad q_*(s',a')]$

# Determining an Optimal Policy

$\pi_*=\underset a{argmax}\quad\sum_{s'}\sum_r P(s',r|s,a)[r+\gamma\cdot v_*(s')]$
$=\underset a {argmax}\quad q_*(s,a)$
- Finding the action providing the best return value