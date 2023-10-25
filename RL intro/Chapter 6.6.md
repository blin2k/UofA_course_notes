# GPI with TD

## The SARSA Algorithm

$S_tA_tR_{t+1}S_{t+1}A_{t+1}$

$Q(S_t,A_t)\leftarrow Q(S_t,A_t)+\alpha (R_{t+1}+\gamma Q(S_{t+1},A_{t+1})-Q(S_t,A_t))$
	Same idea as TD but updating Q instead of V

### The Windy Grid World
![[Pasted image 20231023180506.png]]
	In the windy area, the agent trying to move horizontally will move diagonally.

MC will not perform well in this case, because it updates after the episode finished. Noticing an episode might last for a very long time or forever, so the agent in MC learns slowly or even never learn.

---
# Q-learning

```Q-learning
parameter:
stepsize

initialize:
Q(s,a)

Loop for each episode:
	initialize S
	Loop for each step of episode:
		choose A from S using policy derived from Q (e.g. epsilon-greedy)
		take action A, observe R and S'
		Q(S,A) <- Q(S,A) + stepsize * (R + y* max(Q(S',a)) - Q(S,A))
		S <- S'
until S is terminal
```

- familiar pattern with Q updating
- using `max()` to achieve a greedy move prediction
	- always choose the optimal
	- the difference between SARSA and Q-learning
		- relating SARSA to Bellman Equation
			- [[Chapter 3.5#Bellman Equation Derivation]]
		- relating Q-learning to Bellman Optimality Equation
			- [[Chapter 3.5#Bellman Optimality Equation for $v_*$ and $q_*$]]

# SARSA vs. Q-learning

- SARSA
	- sample-based version of ==policy iteration==
		- using Bellman Equation for action value
		- depends on a ==fixed policy==
- Q-learning
	- sample-based version of ==value iteration==
		- using Bellman Optimality Equation to improve the ==value function==
		- improves the function estimate until converge 

## Q-learning in Windy Grid World

![[Pasted image 20231024164256.png]]
![[Pasted image 20231024164307.png]]

	Noticing that the slope stantds for the number of steps in one episode.

- with step size = 0.5
	- Q-learning converges faster than SARSA
	- seems having a better policy within 8000 time steps
- with step size = 0.1 for SARSA
	- since SARSA needs exploration, large step size results in more penalty
	- they converge to the same optimal policy

---
# Off-policy Q-learning

- SARSA
	- the prediction of the choice of the next action is based on the policy
	- on-policy
- Q-learning
	- the prediction of the choice of the next action is greedy
	- always choose the one seems optimal
	- off-policy
		- target policy
			- greedy
		- behavior policy
			- could be $\epsilon-greedy$ 
	- no importance sampling

![[Pasted image 20231024170712.png]]
- Q-learning learns the optimal value function, so it quickly learns the optimal policy, that is, travel alongside the cliff.
- However, when doing the exploration, travelling alongside the cliff occasionally results in falling off the cliff.
- SARSA learns about its current policy, so it learns to take the longer but more reliable path.
- Avoiding falling into the cliff results in safer path.
---
# Expected SARSA

Instead of sampling the next step, we directly calculate the expected value
- $\sum \pi(a'|S_{t+1})\cdot Q(S_{t+1},a')$

## Stability

Since SARSA updates the action value chosen by the policy, it may choose a wrong direction. 
- after iterations, the expectation will be the same as the true value
- the expected SARSA compute the true value instead of approximation
![[Pasted image 20231024193654.png]]

- low variance
	- update target the exact true value
- expensive
	- spending time on computing averages on every step

## Expected SARSA in Windy Cliff
![[Pasted image 20231024201950.png]]
- overall better
	- reduce randomness
- not affect by step size
	- SARSA may fail to converge when the step size is too large
	- with a small step size, SARSA eventually converge to the same policy as Expected SARSA in long run

## Generality of Expected SARSA

### Off-policy Expected SARSA

Expected SARSA updates the action value regardless of what the next step is. 
Similar to Q-learning which is greedy and regardless of what the next step is in behavior policy,
expected SARSA can be used to learn off-policy.
- no importance sampling

### Greedy Expected SARSA
Noticing that Expected SARSA sums the product of the action value and the probability of the action being chosen under a certain policy.
- when the policy is greedy on action value, it is Q-learning
- Q-learning is a special case of Greedy Expected SARSA