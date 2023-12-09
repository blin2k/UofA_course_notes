# Learning Policies Directly

In the previous chapters, the policy is mostly greedy on action-values. But it is not necessary, for example, the policy can depend on the state only 
- $\pi(Right|s)=1,\quad\pi(Left|s)=1$

## Parameterizing Policies Directly
Same idea as using weights w to learn the action-value $\hat q(s,a,w)$, we can learn $\pi(a|s,\theta)$ where $\theta$ is the parameter.

- constrains
	- $\pi(a|s,\theta)\ge0$ for all $a\in\mathcal A,s\in\mathcal S$
		- all actions have probability to be chosen
	- $\sum_a\pi(a|s,\theta)=1$ for all $\in\mathcal S$
		- the sum of the probabilities of all actions is 1
		- cannot use linear model
			- use SoftMax
				- $\pi(a|s,\theta)\dot=\frac{e^{h(s,a,\theta)}}{\sum_{b\in\mathcal A}e^{h(s,b,\theta)}}$
				- h() can be any score function
				- action preferences
					- it shows how important the action is, but it doesn't related to the return like action value
					- ![[Pasted image 20231207175631.png]]

## Advantages of Policy Parameterization
- the agent can make its policy more greedy over time autonomously
	- the estimates are not that accurate at the beginning, it should be more and more greedy
	- a SoftMax policy can adequately approximate a deterministic policy by making one action preference very large

---
# The Objective for Learning Policies
## Formalizing the Goal as an Objective
- episodic
	- $G_t=\sum^T_{t=0}R_t$
	- the sum of all rewards
- continuing
	- $G_t=\sum^T_{t=0}\gamma^tR_t$
	- $G_t=\sum^T_{t=0}R_t-r(\pi)$
		- average reward formulation
			- $r(\pi)$: average reward
				- $\sum_s\mu(s)\sum_a\pi(a|s,\theta)\sum_{s',r}P(s',r|s,a)\cdot r$
				- expected reward over all actions in all states
			- converge, therefore finite
		- maximize the long-term average of the reward

Thus, we need the gradient of $r(\pi)$
- $\nabla r(\pi)$
	- policy-gradient method
	- we want to maximize it, instead of minimize it like loss function
		- gradient ascent

But there is a problem
- $\nabla_{\theta} r(\pi)=\nabla_\theta\sum_s\mu(s)\sum_a\pi(a|s,\theta)\sum_{s',r}P(s',r|s,a)\cdot r$
	- $\mu$ is the distribution of state s, which depends on $\theta$
 
Not like the case we encounter before 
- $\nabla_w\bar{VE}=\nabla_w\sum_s\mu(s)\left[v_\pi(s)-\hat v(s,w)\right]^2$
	- the distribution is a constant
		- $\sum_s\mu(s)\nabla_w\left[v_\pi(s)-\hat v(s,w)\right]^2$

# The Policy Gradient Theorem

$\nabla r(\pi)=\sum_s\mu(s)\sum_a\nabla\pi(a|s,\theta)q_{\pi}(s,a)$
- the gradient of policy infers the direction of the improvement on a certain action
	- increasing or decreasing the probability to choosing a certain action 

- $\nabla r(\pi)=\mathbb E_\mu\left[\sum_a\nabla\pi(a|s,\theta)q_\pi(s,a)\right]$
	- $\sum_a\pi(a|s,\theta)\frac1{\pi(a|s,\theta)}\nabla\pi(a|s,\theta)q_\pi(s,a)$
	- $\mathbb E_\pi \left[\frac{\nabla\pi(A|S,\theta)}{\pi(A|S,\theta)}q_\pi(S,A)\right]$
- $\theta_{t+1}\dot=\theta_t+\alpha\frac{\nabla\pi(A_t|S_t,\theta_t)}{\pi(A_t|S_t,\theta_t)}q_\pi(S_t,A_t)$
	- $\theta_t+\alpha\nabla ln\pi(A_t|S_t,\theta_t)q_\pi(S_t,A_t)$
		- based on $\nabla ln(f(x))=\frac{\nabla f(x)}{f(x)}$

# Actor-Critic Algorithm
## Approximating the Action Value in the Policy Update

$\theta_{t+1}=\theta_t+\alpha\nabla ln\pi(A_t|S_t,\theta_t)[R_{t+1}-\bar R+\hat v(S_{t+1},w)]$
- actor
	- $s,a+\theta\rightarrow\pi(a|s,\theta)$
- critic
	- $s+w\rightarrow\hat v(s,w)$

$\theta_{t+1}=\theta_t+\alpha\nabla ln\pi(A_t|S_t,\theta_t)[R_{t+1}-\bar R+\hat v(S_{t+1},w)-\hat v(S_t,w)]$
- subtracting the current state's value estimate
	- then the term becomes the TD error $\delta$
	- $\theta_{t+1}=\theta_t+\alpha\nabla ln\pi(A_t|S_t,\theta_t)\delta_t$
	- it doesn't affect the update but reduces the update variance
	-  ![[Pasted image 20231208191937.png]]
	- ![[Pasted image 20231208192513.png]]

# Policy Parameterizations

## Actor-Critic with SoftMax Policies

critic
- $\theta\leftarrow \theta+\alpha^\theta\nabla ln\pi(A|S,\theta)\delta$
	- $\pi(a|s,\theta)=\frac{e^{h(s,a,,\theta)}}{\sum_{b\in\mathcal A}e^{h(s,b,\theta)}}$
	- using SoftMax as the policy
	- $\nabla ln\pi(a|s,\theta)=x_h(s,a)-\sum_b\pi(b|s,\theta)x_h(s,b)$

actor
$w\leftarrow w+\alpha^wx(s)\delta$
- $\hat v(s,w)=w^Tx(s)$
	- $\nabla\hat v=x(s)$
- $h(s,a,\theta)=\theta^Tx_h(s,a)$
	- $x_h$ needs both state and action
	- stack state features

## Gaussian Policies for Continuous Actions

Using probability density where the probability is the area under the curve and above the interval. 
- more specifically, using Normal distribution
	- $\pi(a|s,\theta)=\frac{1}{\sigma(s,\theta)\sqrt{2\pi}}exp(-\frac{(a-\mu(s,\theta))^2}{2\sigma(s,\theta)^2})$
		- $\mu(s,\theta)=\theta_\mu^Tx(s)$
			- it can be any function, but we choose a linear model of state features here
		- $\sigma(s,\theta)=exp(\theta^T_\sigma x(s))$
			- the variance must be positive
- $\theta=[\theta_\mu,\theta_\sigma]^T$
	- $\nabla ln\pi(a|s,\theta_\mu)=\frac1{\sigma(s,\theta)^2}(a-\mu(s,\theta))\cdot x(s)$
	- $\nabla ln\pi(a|s,\theta_\sigma)=(\frac{(a-\mu(s,\theta))^2}{\sigma(s,\theta)^2}-1)\cdot x(s)$

advantages of continuous action
- it might not be straightforward to choose a proper discrete set of actions
	- how hard should the agent hit the ball
- continuous actions allow us to generalize over actions