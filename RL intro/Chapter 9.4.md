# Parameterized Functions

## Linear Value Function Approximation
$\hat v(s,w)\dot=\sum w_ix_i(s)=<w,x(s)>$

$\hat v(s,w)\dot=w_1X+w_2Y$
can be used to describe the states on a X times Y board

## Nonlinear Function Approximation

- Neural Network

---
# Generalization and Discrimination

- generalization
	- updates to the value estimate of one state influence the value of other states
	- important for fast learning
- discrimination
	- the ability to make the value of two states different

Tabular representation
- good discrimination
- no generalization

---
# Framing Value Estimation as Supervised Learning

The state is the features.

- MC
	- $(S_i,G_i)$
- TD
	-  $(S_i,R_i+\gamma \cdot\hat v(S_i,w))$


- online setting
	- the agent interacts with an environment and continually generates new data
- offline setting
	- the full dataset is available from the start and remains fixed throughout the learning

The function approximator should be compatible with online updates and bootstrapping.

## The Value Error Objective

- mean squared value error
	- $\bar{VE}=\sum_s \mu(s)[v_\pi(s)-\hat v(s,w)]^2$
		- $\mu$: the fraction of time we spend in S when following policy $\pi$
		- small $\mu$ means we can have higher error
 ![[Pasted image 20231120215357.png]]

## Gradient Descent

- linear value function
	- $\hat v(s,w)=\sum w_ix_i(s)$
	- $\frac{\partial \hat v}{\partial w_i}=x_i(s)$
	- $\nabla \hat v=x(s)$

$w_{t+1}=w_t-\alpha\nabla J(w_t)$

## Gradient Monte for Policy Evaluation
$$\begin{align}
&\nabla \sum_s\mu(s)\cdot[v_\pi(s)-\hat v(s,w)]^2\\
&=\sum_s\mu(s)\cdot\nabla[v_\pi(s)-\hat v(s,w)]^2\\
&=\sum_s\mu(s)2\cdot[v_\pi(s)-\hat v(s,w)]\cdot\nabla \hat v(s,w )\\
\end{align}$$
$w_{t+1}=w_t+\alpha[G_t-\hat v(s_t,w_t)]\nabla\hat v(s,w_t)$
- replace $v_\pi$ with Gt because $v_\pi=\mathbb E[G_t|S_t=s]$

```pseudo
input:
policy - pi
differentiable function - v_bar
step size - alpha > 0
arbitrarily initilaized value function weights - w

LOOP FOREVER (for each episode)
	generate an episode S0, A0, R1, S1, A1,...,RT, ST using pi
	LOOP for each step of episode, t = 0, 1,..., T-1
		w <- w + alpha * [Gt - v_bar(ST, w)] * nabla(v_bar(ST,w))
```

## State Aggregation with MC

Aggregate similar states, so when one of them is updated, all of them will be updated.
- speed up the learning process

## Semi-Gradient TD for Policy Evaluation

$w\leftarrow w+\alpha[U_t-\hat v(S_t,w)]\nabla\hat v(S_t,w)$
- Ut unbiased -> w will converge to a local optimum
- $U_t\dot=R_{t+1}+\gamma\hat v(S_{t+1},w)$
	- TD target
	- biased -> w ==may not== converge to a local optimum

$\nabla\frac12[U_t-\hat v(S_t,w)]^2$
$=(U_t-\hat v(S_t,w))(\nabla U_t-\nabla\hat v(S_t,w))$
$\not=-(U_t-\hat v(S_t,w))\nabla\hat v(S_t,w)$
- only equal when Ut = 0
	- but for TD, $U_t=\nabla(R_{t+1}+\gamma\hat v(S_{t+1},w)=\gamma\nabla\hat v(S_{t+1},w)\not=0$
- TD is a semi-gradient method

```pseudo
input:
pi
v_hat
stepsize
w

LOOP for each episode
	initialize S
	LOOP for each step of episode
		choose A~pi(S)
		take action A, observe R, S'
		w <- w + stepsize*[R+gamma*v_hat(S',w)-v_hat(S,w)]*nabla(v_hat(S,w))
		S <- S'
	until S is terminal
```

## Comparing TD and MC with State Aggregation

MC takes Gt as the true value while TD takes the predicted return of the next state.

TD will converge faster but may not converge to a local optimum

---
# Linear TD

$w\leftarrow w+\alpha\delta_t\nabla\hat v(S_t,w)=w+\alpha\delta_t x(S_t)$
- $\delta_t=R_{t+1}+\gamma\hat v(S_{t+1},w)-\hat v(S_t,w)$
- $\hat v(S_t,w)=w^Tx(S_t)$
- $\nabla \hat v(S_t,w)=x(S_t)$

Tabular TD is a special case of Linear TD.

# The True Objective for TD

![[Pasted image 20231122190817.png]]

The TD Fixed Point
- $\mathbb E[\Delta w_{TD}]=\alpha(b-Aw_{TD})=0$
- $\Rightarrow w_{TD}=A^{-1}b$
- $w_{TD}$ minimizes $(b-Aw)^T(b-Aw)$ 

$\bar{VE}(w_{TD})\le\frac1{1-\gamma}min_w \bar{VE}(w)$
- value error

