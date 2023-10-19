# Multi-armed Bandits

RL uses training information that ==evaluates== the actions taken rather than ==instructs== by giving correct actions. 
	This is what creates the need for active exploration, for an explicit search for good behavior.

---
# Estimating Action Selection

## Sample-Average Method
$Q_t(a)\dot=\frac{\sum^{t-1}_{i=1}R_i}{t-1}$  

## Action Selection
- Greedy Action
	- The action that currently has the largest estimated value
	- $\underset a{argmax}\,Q(a)$
### Incremental Update Rule
- $Q_{n+1}=\frac1n\sum^n_{i=1}R_i=Q_n+\frac1n(R_n-Q_n)$
	- $NewEstimate\leftarrow OldEstimate+StepSize(Target-OldEstimate)$ 
	- $\alpha\dot=StepSize=\frac1n$ 
- To Nonstationary Problems
	- Use a fixed step size, then the most recent rewards affect the estimate more than older rewards, because the step size remains instead of decreases with time
- $Q_{n+1}=Q_n+\alpha_n(R_n-Q_n)=(1-\alpha)^nQ_1+\sum^n_{i=1}\alpha(1-\alpha)^{n-i}R_i$ 
	- The contribution of Q1 decreases exponentially with time
	- The rewards further back in time contribute exponentially less to the sum

### $\epsilon$-Greedy Action Selection
- Balancing exploration and exploitation
$$
A_t\leftarrow
\begin{cases}
\underset a{argmax}\,Q_t(a) & \text{with probability }1-\epsilon\\
a~Uniform(\{a_1...a_k\}) & \text{with probability }\epsilon
\end{cases}
$$
- Greedy or Random

### Optimistic Initial Values
- Setting Q1 a very optimistic value, then even the trial succeed, the estimates decreases, but the penalty is smaller than failing the trial  
- explore all
- not well-suited for nonstationary problems

### Upper-Confidence Bound Action Selection
Uncertainty in Estimates
	how wide is the range that the true value lays in around the estimated value

- The agent optimistically picks the action that has the highest upper bound
	1. it does have the highest value, or
	2. learn about an action we know least about
- $A_t\dot=\left[Q_t(a)+c\sqrt{\frac{ln\,t}{N_t(a)}}\right]$ 
	- highest estimated value + UCB exploration term
	- with time goes, $ln\,t$ increases. if $N_t(a)$ is large, that is it is selected a lot, the term will be relatively small, then the agent is likely to explore an action that is seldom selected