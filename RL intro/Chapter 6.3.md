# Temporal Difference

$$\begin{align}
V(S_t)&\leftarrow V(S_t)+\alpha[G_t-V(S_t)]\\
&= V(S_t) +\alpha[R_{t+1}+\gamma\cdot V(S_{t+1})-V(S_t)]
\end{align}$$
In this way, we don't have to wait till the end of the episode to get the return value, instead, we take the reward and value of the next state.

Let's call this term TD error $\delta_t=R_{t+1}+\gamma V(S_{t+1})-V(S_t)$

The idea of taking advantage of the next state is similar to what we do in [[Chapter 4#Value Iteration]] where we average all possible next states.

```tabular TD(0) for estimating v_pi
input:
pi

parameter:
stepsize

initialize:
# a complete value table
V(s) for all s

Loop for each episode:
	initialize S
	Loop for each step of episode:
		A <- acton given by pi for S
		take action A and observe R, S'
		V(S) <- V(S) + stepsize * [R + yV(S') - V(S)]
		S <- S'
	until S is terminal
```

## Advantage

Unlike DP, TD do not require a model of the environment.
- it only needs the information of next state

Unlike MC, TD do not need to wait till the end of the episode
- it can update the values every step
- converge faster than MC

## TD vs. MC

![[Pasted image 20231022174346.png]]
larger learning rate $\alpha=0.15$
- converge faster
- higher final error

smaller learning rate $\alpha=0.05$
- converge slower
- lower final error