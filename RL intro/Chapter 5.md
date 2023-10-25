# Intro to Monte Carlo Methods

- in some problems, we don't know the environment transition probabilities
- the computation can be error-prone and tedious

We need Monte Carlo.
- averaging over a large number of random samples

Similar to the bandit problem, which valuates a bandit as its average value over trials, MC valuates the return G of a state as the average return over episodes.

---
To compute all returns of a episode, it is efficient to do it in a dynamic programming way since every return includes the next return.

```MC prediction V
input: 
pi

initialize:
V(s)
Returns(s) <- empty list

Loop forever(for each episode):
	generate an episode following pi: S0, A0, R1,...,St-1, At-1, Rt
	G <- 0
	Loop for each step of episode, t = t-1,...,0
		G <- yG + Rt+1
		append G to Returns(St)
		V(St) <- average(Returns(St))
```


For better comprehension, you can ignore the last line since it does not affect the returns list.

The 2nd loop computes the return value from the last step to the first step, and append them to the returns list one by one.

The 1st loop makes sure every episode will generate a return list.

---
Incremental Update: 
$NewEstimate\leftarrow OldEstimate+StepSize[Target-OldEstimate]$

---
# Using MC for Prediction
 ![[Pasted image 20231020191013.png]]

---
# Using MC for Action Value

Some actions are never selected, then we have no way to know the return value by averaging data.

We solve this by implementing exploration.

## Exploring Starts

Guarantee episodes start in every state-action pair, it follows the policy after.

---
# Using MC for GPI (Generalized Policy Iteration)

Policy Iteration repeat generates new policies at least as good as the old policy.

The improvement rule can be simply greedy at action value:
- $\pi_{k+1}(s)=\underset a{argmax}\quad q_{\pi_k}(s,a)$

For the evaluation part, we use MC prediction.

	In every state, always choose the action with the greatest return value. It will update the return value after an episode, then the agent may choose different action next time since it is greedy.

```MC ES
initialize:
pi(s)
Q(s,a)
Returns(s,a) <- empty list

Loop forever (for each episode):
	# Exploring Starts
	choose S0, A0 randomly and let all pairs have probability > 0
	generate an episode from S0,A0 following pi
	G <- 0
	# Monte Carlo
	Loop for each step of episode
		G <- yG + Rt+1
		append G to Returns(St,At)
		Q(St,At) <- average(Returns(St,At))
		pi(St) <- argmax Q(St,a)
```

---
# Epsilon-Soft Policies

Sometimes, we cannot initialize all possible state-action pair. 
- e.g. self-driving: every possible position of the road

$\epsilon-Greedy\subset\epsilon-Soft$
- assign all action a probability $\frac\epsilon{|\mathcal A|}$
	- no need for Exploring Start anymore
	- thus stochastic
- may not be optimal
	- can only find the optimal $\epsilon-soft$ policy
	- worse than $\pi_*$
 
```MC control (for epsilon-soft)
parameter:
small epsilon > 0

initialize:
pi <- arbitrary epsilon-soft policy
Q(s,a)
Returns(s,a) <- empty list

Loop forever (for each episode):
	generate episode following pi
	G <- 0
	Loop for each step of episode:
		G <- yG + Rt+1
		append G to Returns(St, At)
		# Monte Carlo
		Q(St,At) <- average(Returns(St,At))
		# Greedy
		A* <- argmax Q(St,a)
		for all a in A(St):
			if a = A*:
				# updating the possibility of choosing the greedy choice
				pi(a|St) <- 1-epsilon + epsilon/|A(St)|
			else:
				# updating the possibility of chossing a non-greedy choice
				pi(a|St) <- epsilon/|A(St)|
```

---
# On-Policy vs. Off-Policy

- On-Policy
	- improve and evaluate the policy being used to select actions
- Off-Policy
	- improve and evaluate a ==different== policy from the one used to select actions
	- learning an optimal policy from suboptimal policy

## Behavior Policy

$b(a|s)$
- select actions from this policy
- generally an ==exploratory== policy
- different from the target policy $\pi(a|s)$
	- covers $\pi$
		- $\pi(a|s)>0\rightarrow b(a|s)>0$

On-Policy
- $\pi(a|s)=b(a|s)$

---
# Importance Sampling

- sample: $x\sim b$
- estimate: $\mathbb E_\pi[X]$

$$\begin{align}
\mathbb E_\pi[X]&\dot=\sum x\cdot \pi(x)\\
&=\sum x\cdot \frac{\pi(x)}{b(x)}\cdot b(x)\\
&=\sum x\cdot \rho(x)\cdot b(x)\\
&=\mathbb E_b[X\cdot\rho(X)]\\
&\approx \frac1n \sum x_i\cdot \rho(x_i)
\end{align}
$$
Recall that $\mathbb E_\pi[X]=\frac1n\sum x_i$

---
# Off-Policy MC Prediction

Because of
- $x\sim b$

Instead of averaging return values of the same action, we need to average $\rho G_t$
- $V_\pi(s)=\mathbb E_b[\rho G_t|S_t=s]$

$P(\text{trajectory under b})=P(A_t,S_{t+1},A_{A+1},...,S_T|S_t,A_{t:T})=\prod^{T-1}_{i=t} b(A_i|S_i)\cdot P(S_{i+1}|S_i,A_i)$
	The probability of a specific path from the given state equals,
	the probability of having a specific action under the behavior policy
	times the probability of having a specific next state.

	All pairs are specific because the path we are talking about is specific.

 $\rho_{t:T-1}\dot=\frac{P(\text{trajectory under }\pi)}{P(\text{trajectory under b})}=\prod^{T-1}_{k=t}\frac{\pi(A_k|S_k)\cdot P(S_{k+1}|S_k,A_k)}{b(A_k|S_k)\cdot P(S_{k+1}|S_k,A_k)}=\prod^{T-1}_{k=t}\frac{\pi(A_k|S_k)}{b(A_k|S_k)}$ 
 
```Off-Policy MC
input:
pi

initialize:
V(s)
Returns(s) <- empty list

Loop forever (for each episode):
	generate an episode following b
	G <- 0
	# initialize the ratio to 1
	W <- 1
	Loop for each step of episode:
		G <- yWG + Rt+1
		append G to Returns(St)
		V(St) <- average(Returns(St))
		# recursively updating it makes the product shown above
		W <- W * pi(At|St) / b(At|St)
```

