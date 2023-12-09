# Episodic SARSA with Function Approximation

In the previous chapter, we linearly approximate the value function. We can do that on the action-value function too, with an extra input a.

## How to Represent Actions?

One way to do this is to repeat each feature to represent that feature taking different actions.
- feature representation stack
![[Pasted image 20231206212936.png]]
- the weights for one action value do no interact with those of another action value

![[Pasted image 20231206215443.png]]

# Expected SARSA with Function Approximation

$w\leftarrow w+\alpha\left(R_{t+1}+\gamma\sum_{a'}\pi(a'|S_{t+1})\cdot \hat q(S_{t+1},a',w)-\hat q(S_t,A_t,w)\right)\cdot\nabla \hat q(S_t,A_t,w)$

## Expected SARSA to Q-learning

$w\leftarrow w+\alpha\left(R_{t+1}+\gamma max_{a'}\hat q(S_{t+1},a',w)-\hat q(S_t,A_t,w)\right)\cdot\nabla\hat q(S_t,A_t,w)$

# Exploration under Function Approximation

Initialize values optimistically under function approximation
- linear
	- set the weight to be the largest possible return
	- as long as the state has at least one feature active, the value will be optimistic and likely overly so
	- it will learn to be reduce
- non-linear
	- difficult to initialize weights optimistically

# Average Reward
![[Pasted image 20231206225845.png]]
Larger gamma may result in larger and more variables sums, which might be difficult to learn.

The average reward objective
- $r(\pi)\dot=\underset{h\rightarrow \infty}{lim}\,\frac1h\sum_{t=1}^h\mathbb E\left[R_t|S_0,A_{0:t-1}\sim\pi\right]$
	- $\sum_s\mu_{\pi}(s)\sum_a\pi(a|s)\sum_{s',r}P(s',r|s,a)r$
- ![[Pasted image 20231206230545.png]]

Returns for average reward

